# Audit — MIP-Collections-ERC721

**Date:** 2026-06-20
**Status:** Deployed — v0.4.0 (royalties + audit fixes live)
**Toolchain:** OpenZeppelin v0.20.0, Cairo/Starknet 2.12.0, snforge 0.59.0
**Files:** `IPCollection.cairo` (registry/factory), `IPNft.cairo` (per-collection ERC-721),
`types.cairo`, `interfaces/IIPCollection.cairo`, `interfaces/IIPNFT.cairo`

## Deployment

Chain is a first-class dimension; today's deployment lives on **Starknet** (on-chain
`version() == "0.4.0"`). This is the address apps should adopt:

| Component | Chain | Value |
|---|---|---|
| `IPCollection` registry | Starknet | `0x0558c9b6ea4d403df6d765fb77be55702c572f0a811f037c6c4209fe1e5aeef2` |
| `IPCollection` class hash | Starknet | `0x063d4ac4ae317fd155216bf1b8a4d3a63172ff72965b9ac48dd5add0c2d32b70` |
| `IPNft` class hash | Starknet | `0x040551f0d009a6d665ddff980a375dfccc71a8928c8bfcc9ab56244bc4464fab` |

Verified post-deploy: `get_collection_count() == 0`, `version() == "0.4.0"`.

## Overall assessment

The contract is **sound**. It is immutable by construction (no owner / admin / upgrade / pause),
mint and archive are strictly registry-gated, transfer paths (single and batch) require both
contract approval and caller authorization, token IDs are monotonic and never reused, and the
record fields are write-once. Prior audit fixes (`COMP-`, `R-`, `M-`, `H-`, `C-`, `L-` tags) are
present and correct.

**No Critical or High findings.** The headline item is a **missing feature** (royalties), plus two
low-risk optimizations. One earlier concern (archive irreversibility) is **withdrawn** — it is
correct by design.

## Findings

| # | Severity | Item | Action |
|---|---|---|---|
| F-1 | Feature gap | No EIP-2981 → zero royalty on secondary sales | Add per-token EIP-2981 (this redeploy) |
| D-1 | Low (defense-in-depth) | CEI violation: `mint`/`batch_mint` write `total_minted` **after** the external `ip_nft.mint` call | Write effect before interaction; pin "no receiver callback" as a tested invariant |
| D-2 | Low | `batch_mint` event (`TokenMintedBatch`) omits per-token `metadata_uri` | Add `metadata_uris` to the event |
| D-3 | Info | `total_transfers` counts only registry-routed transfers (silently partial) | Rename `protocol_routed_transfers`, or derive from `Transfer` events |
| O-1 | Low (opt) | Stringified `"collection_id:token_id"` token API → per-call parse cost + surface | Take `(collection_id, token_id): u256` |
| O-2 | Low (opt) | `get_contract_address()` re-fetched inside the `batch_transfer` loop | Hoist out of the loop |
| O-3 | Minor (opt) | `transfer_token`'s `from` arg is redundant (must equal `owner_of`) | Drop the arg, derive it |
| ~~M-1~~ | Withdrawn | Archive is irreversible | **By design — no change** |

### D-1 — Checks-Effects-Interactions in mint / batch_mint

`IPCollection.mint` calls `ip_nft.mint(...)` **before** writing `collection_stats.total_minted`
(`batch_mint` advances `total_minted` only after its loop). This is safe **today only because
`IPNft` uses `mint`, not `safe_mint`** — there is no `IERC721Receiver` callback to re-enter on. If
mint ever becomes `safe_mint`, or any external call is added before the write, a reentrant call
reads a stale `total_minted` and mints a **colliding token ID**. Fix: write `total_minted` before
the external call (a revert rolls it back regardless). Add an explicit, tested invariant: *IPNft
mint must never invoke a receiver callback.* Latent, not exploitable in the current code — but it is
the failure mode that silently becomes a High on a future "improvement".

### D-2 — Batch mint event asymmetry

`TokenMinted` (single) carries `metadata_uri`; `TokenMintedBatch` carries only
`token_ids`/`owners`/`operator`/`timestamp`. An indexer-independent, event-only reader (the model
the protocol must support) cannot reconstruct batch-minted URIs from logs and must fall back to
per-token `token_uri` reads. URIs are not lost (they live on-chain), but the event stream is
asymmetric — add `metadata_uris` to the batch event.

### D-3 — Partial transfer counter

`total_transfers` increments only on registry-routed transfers; direct ERC-721 `transfer_from`
bypasses it (`types.cairo:104`). A silently-partial counter on a source-of-truth contract is
misleading; rename it `protocol_routed_transfers` or drop it and derive from standard `Transfer`
events.

### F-1 — EIP-2981 royalties (the urgent gap)

The marketplace pays royalties by reading EIP-2981 `royalty_info` off the NFT at settlement. The
MIP collection never exposed it, so creators' declared "Royalty %" lives only in IPFS metadata and
is **never paid** on resale. Required design (consistent with `05-licensing §43-52` "royalty splits
on settlement" and `contract-design-conventions §87` "register `IERC2981_ID` when royalties
exist"):

- Add OZ `ERC2981Component` to **`IPNft`** (the queried token contract), register `IERC2981_ID` in
  the constructor, expose snake_case `royalty_info`.
- Extend `mint(... , royalty_bps)`; internally `_set_token_royalty(token_id, creator, royalty_bps)`.
- **Receiver = the token's immutable `original_creator`**, never the (mutable) collection owner —
  ownership can transfer; the creator/royalty receiver must not silently follow it.
- **Set once at mint, no public setter** — mount `ERC2981InternalImpl` only, **not**
  `ERC2981AdminOwnableImpl`. Satisfies `contract-design-conventions §51` ("economic terms are
  immutable… royalty never changes after creation; new terms = new record"). Stricter than the
  ERC-1155 collections precedent, which left royalty owner-mutable.
- Bound `assert(royalty_bps <= 10000)` in-contract (protocol-neutral); the app keeps its 50% cap.
- Thread `royalty_bps` through `IPCollection.mint` / `batch_mint` → `IPNft.mint`.
- **Royalty receiver = creator only. No protocol fee** (`contract-design-conventions §55`).
- **Permanent by design.** Per-token royalty is immutable (no setter), so a creator cannot lower it
  later. The app must disclose this at mint ("royalty is permanent") and keep its 50% input cap.
  Resellers are protected at settlement by the seller-signed `royalty_max_bps`, not by the
  collection — so the contract bound stays the standard `≤ 10000`.

### O-1 — Replace the stringified token identifier

`archive`, `batch_archive`, `transfer_token`, `batch_transfer`, `get_token`, `is_valid_token`,
`is_transferable_token` take a `ByteArray` `"collection_id:token_id"` and run
`TokenTrait::from_bytes` (byte loop + two decimal→u256 parses) per token, per call. Taking
`(collection_id: u256, token_id: u256)` deletes `from_bytes`/`bytearray_to_u256`, removes an
input-validation surface, and saves gas on every token op. Best done now (ABI break + SDK migration
already happening).

### O-2 — Hoist `get_contract_address()` in `batch_transfer`

`registry` is invariant but re-fetched each loop iteration (`IPCollection.cairo:504`). Hoist it out,
matching the already-hoisted `caller`/`timestamp`.

## Immutability invariants (verified — keep bulletproof)

The legal value (Berne-aligned authorship, durable ownership) depends entirely on immutability. The
audit's job is to prove these hold, not relax them. All are covered by tests:

| Invariant | Test |
|---|---|
| Record fields (URI, creator, timestamp) write-once | `test_collection_metadata_is_immutable_after_creation`, `test_token_data_includes_creator_and_timestamp`, `test_token_uri_match` |
| Archive preserves the record | `test_archive_preserves_record` |
| Archived tokens are permanently immobile (both paths) | `test_archived_token_transfer_blocked`, `test_direct_erc721_transfer_archived_token_blocked`, `test_is_transferable_token_false_after_archive` |
| Creator never changes on ownership transfer | `test_creator_unchanged_after_transfer` |
| Mint authority strictly the registry / collection owner | `test_mint_not_owner`, `test_previous_collection_owner_cannot_mint_after_transfer`, `test_mint_zero_caller` |
| No admin / owner / upgrade / pause path | structural — no such entrypoint exists |

When adding EIP-2981, add tests: royalty is set at mint, receiver == `original_creator`, royalty is
not mutable post-mint, `bps > 10000` rejected, `royalty_info` returns the expected split,
`IERC2981_ID` is discoverable via SRC5.

## On-chain enumeration — KEEP (decision)

`user_collections` / `user_collection_index` (registry) and `ERC721Enumerable` (`IPNft`) are
**retained**. The contract is the source of truth and must answer "what does this address own?"
**without any external indexer**. Enumeration here is over already-public data (no privacy
implication — see `2026-06-20-enumeration-regression-plan.md`); its only cost is gas, which a public
IP registry rightly pays. This **reverses** the prior "remove enumeration" reasoning.

Bookkeeping is covered by `test_transfer_collection_ownership_updates_owner_collection_lists`,
`test_user_collections_mapping`, `test_get_all_user_tokens` — keep these; the swap-remove path in
`transfer_collection_ownership` must stay consistent across `user_collections`,
`user_collection_index`, `collection_owner_index`.

## What was NOT found

No reentrancy (IPNft is registry-deployed with a fixed class hash → trusted; `mint`/`transfer_from`
have no receiver callbacks), no access-control gaps, no token-ID reuse, no integer-overflow exploit,
no admin/upgrade backdoor.

## Remediation / redeploy

Single breaking redeploy carries: F-1 (royalties), D-1/D-2/D-3, O-1/O-2/O-3, and the already-pending
`mint(creator)` change.

1. ✅ **Implemented + tested (2026-06-20).** F-1 (per-token EIP-2981, receiver = creator, no setter,
   `IERC2981_ID` registered), D-1 (CEI reorder in `mint`/`batch_mint` + "no receiver callback"
   invariant comment), D-2 (`metadata_uris` in batch event), D-3 (`protocol_routed_transfers`
   rename), O-1 (`(collection_id, token_id): u256` args; stringified-token parser removed), O-2
   (hoisted `get_contract_address` in `batch_transfer`), O-3 (dropped redundant `from` from
   `transfer_token`). `scarb build` clean; **63/63 `scarb test` passing** (incl. new royalty tests:
   royalty set at mint, receiver unchanged after transfer, zero-royalty, `>10000` rejected,
   `IERC2981_ID` discoverable).
2. ✅ **Declared + deployed on mainnet (2026-06-20, v0.4.0)** via profile `medialane-mainnet`:
   - `IPNft` class: `0x040551f0d009a6d665ddff980a375dfccc71a8928c8bfcc9ab56244bc4464fab`
   - `IPCollection` class: `0x063d4ac4ae317fd155216bf1b8a4d3a63172ff72965b9ac48dd5add0c2d32b70`
   - `IPCollection` registry: `0x0558c9b6ea4d403df6d765fb77be55702c572f0a811f037c6c4209fe1e5aeef2`
   - Verified: `get_collection_count() == 0`, `version() == "0.4.0"`.
   - `version()` (ByteArray) added to `IPCollection` + `IPNft` per the house convention (matches
     the ERC-1155 collections pattern); `Scarb.toml` bumped to `0.4.0`; 64/64 tests pass.
3. Migrate the ABI platform-wide: SDK (mint calldata + `royalty_bps`; `(collection_id, token_id)`
   args; per-token `royalty_bps` array on `batch_mint`), backend, dapp, io (wire the form's
   royalty % → bps).
4. Point apps at the new factory; collections on the old class become external/legacy (no patching).
