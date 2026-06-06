# IP-Time-Capsule - Audit & Redesign Report

**Date:** 2026-05-25  
**Scope:** `contracts/IP-Time-Capsule`  
**Status:** Redesigned and tested

---

## Executive Summary

The legacy IP Time Capsule contract did not satisfy the original briefing or Medialane first principles. It was nominally permissionless, but it also included owner/admin upgradeability, stored reveal material in a way that did not provide real secrecy, used unsafe minting, duplicated enumerable token tracking with fragile custom lists, and lacked clear service discovery.

The redesigned contract is a narrower, safer ERC-721 service:

- permissionless minting,
- no owner, no admin, no upgradeability,
- OpenZeppelin ERC-721 + Enumerable + SRC5,
- hidden `token_uri` until reveal,
- encrypted payload pointer and salted content commitment at mint,
- authorized reveal by creator or current owner after `reveal_at`,
- content-addressed URI policy for hidden, encrypted, and revealed metadata.

## Architecture Alignment

| Principle | Result |
|---|---|
| Contract is the only truth | Capsule state, reveal status, owner, creator, timestamps, and events live on-chain. |
| Permissionless | Any caller can mint to any recipient. No allowlist or admin gate exists. |
| Interoperability | Assets are standard ERC-721 NFTs with OpenSea-compatible `token_uri`. |
| Selective enforcement | Time-lock is explicit service-level enforcement, appropriate for this service. |
| Protocol/app split | No fee logic, no platform roles, no indexer authority. |
| Service model | Registers `IIP_TIME_CAPSULE_ID` for SDK/indexer/agent discovery. |

## Legacy Findings

| Severity | Finding | Resolution |
|---|---|---|
| High | Plain reveal data was represented as on-chain metadata before unlock. On-chain storage is public, so this does not provide privacy. | New design stores only `encrypted_uri` and salted `content_commitment` before reveal; plaintext URI is written only in `reveal_capsule`. |
| High | Contract included `OwnableComponent` and `UpgradeableComponent`, giving an admin upgrade path over supposedly permanent IP records. | Removed owner and upgradeability entirely. |
| High | Mint used `mint` instead of `safe_mint`, risking locked NFTs when the recipient is a non-receiver contract. | Replaced with `safe_mint` and added receiver/account tests. |
| Medium | Custom `user_tokens` list duplicated ERC721 enumerable behavior and attempted manual transfer bookkeeping. | Removed custom owner-token storage; uses OpenZeppelin enumerable. |
| Medium | `set_metadata` allowed post-unlock mutation of metadata, weakening the capsule's integrity. | Replaced with one-time `reveal_capsule`; reveal cannot be changed. |
| Medium | No service-specific SRC5 interface registration. | Added `IIP_TIME_CAPSULE_ID`. |
| Low | Dependency versions were broad/old and Alexandria was only needed for custom lists. | Pinned Starknet/OZ-compatible versions and removed Alexandria. |
| Low | Tests relied on owner-like caller assumptions and did not cover safe mint, reveal authorization, event payloads, or interface support. | Replaced with 30 tests covering mint, reveal, URI policy, enumerable, safe mint, SRC5, and events. |

## Privacy & Commitment Model

The phrase "metadata remains encrypted until the reveal date" cannot mean "the contract encrypts data." Smart contracts cannot keep secrets once data is submitted on-chain.

The redesigned model is:

1. `encrypted_uri`: content-addressed pointer to encrypted/off-chain sealed payload.
2. `content_commitment`: creator's original salted commitment to the eventual plaintext content.
3. `hidden_uri`: public placeholder metadata returned by `token_uri` before reveal.
4. `revealed_uri`: content-addressed plaintext metadata pointer written only after unlock.
5. `content_hash`: reveal-time hash of the final plaintext metadata or payload.
6. `content_salt`: reveal-time salt used to prove the original commitment.

The canonical commitment is:

```text
content_commitment = Poseidon(content_hash, content_salt)
```

The contract enforces timing, one-time reveal, authorization, and commitment equality. Clients/indexers should verify that the content resolved from `revealed_uri` hashes to the revealed `content_hash`.

## Contract Surface

| Function | Purpose |
|---|---|
| `mint_capsule` | Mints a sealed time capsule NFT. |
| `reveal_capsule` | Reveals the final metadata after `reveal_at`. |
| `get_capsule_data` | Returns full capsule state plus current ERC-721 owner. |
| `get_encrypted_uri` | Returns the encrypted/sealed payload URI. |
| `get_revealed_uri` | Returns revealed URI, reverting before reveal. |
| `get_token_creator` | Returns immutable creator/minter. |
| `get_token_reveal_at` | Returns unlock timestamp. |
| `is_unlocked` | Returns whether current block time is at or after `reveal_at`. |
| `is_revealed` | Returns whether reveal has occurred. |
| `get_hidden_uri` | Returns placeholder metadata URI. |
| `get_max_lock_duration` | Returns constructor-set maximum lock window. |
| `compute_content_commitment` | Returns `Poseidon(content_hash, content_salt)`. |
| `get_commitment_scheme` | Returns `COMMITMENT_SCHEME_POSEIDON_HASH_SALT`. |

## Test Results

```text
Collected 30 test(s)
Tests: 30 passed, 0 failed, 0 ignored, 0 filtered out
```

Coverage includes:

- deployment metadata,
- permissionless mint,
- IPFS and Arweave URI policy,
- zero recipient rejection,
- empty commitment rejection,
- future/max reveal timestamp checks,
- locked/unlocked state,
- reveal authorization,
- content commitment mismatch rejection,
- empty reveal salt rejection,
- one-time reveal,
- mint and reveal event payloads,
- token URI transition from hidden to revealed,
- transfer before reveal,
- enumerable behavior,
- safe mint to receiver contracts,
- rejection of non-receiver contracts,
- SRC5 interface support,
- nonexistent token guards.

## Remaining Integration Notes

- The service registry should declare this as a future `ip-time-capsule` service with capabilities `mint`, `transfer`, and a time-lock enforcement declaration:

```ts
{
  id: "ip-time-capsule",
  displayName: "IP Time Capsule",
  standard: "ERC721",
  provenance: "MEDIALANE",
  uiVariant: "time-capsule",
  capabilities: ["mint", "transfer"],
  metadataSchema: {
    requiredTraits: ["Time Lock", "Reveal Date", "Commitment Scheme"],
    licenseDefault: "CC BY-SA",
    enforcement: { timeLock: true },
  },
}
```

- The SDK/indexer should expose the privacy caveat plainly: encrypted payloads and commitments are public; plaintext must not be submitted until reveal.
- Indexers should persist `TimeCapsuleMinted` and `TimeCapsuleRevealed` events and derive `sealed`/`revealed` state from chain events plus `get_capsule_data`.
- Off-chain tooling should compute `content_hash` deterministically, keep `content_salt` private until reveal, and call `compute_content_commitment` or mirror its Poseidon formula before mint.
