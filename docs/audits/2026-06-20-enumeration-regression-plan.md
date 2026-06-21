# Audit Plan — On-Chain Enumeration / "Data-Minimization" Regression

**Date:** 2026-06-20
**Status:** Open
**Owner:** Rodrigo + Claude

## What went wrong

A principle was over-generalized in the foundations and propagated through several
contract audits:

> *"No on-chain enumeration structures (rosters, per-user ID vectors, ERC721Enumerable).
> Indexers rebuild views from keyed events; data not held cannot be compelled."*

This was used to **delete real on-chain features** (subscriber rosters, per-user token/collection
enumeration) from production-grade contracts, justified as *privacy / data minimization*.

**The reasoning is wrong.** On-chain state is public by definition. Token ownership is already
public via `owner_of` + `Transfer` events; subscriptions are already public via payment transfers +
events. An enumeration index over that data **exposes nothing new** — so "data not held cannot be
compelled" does not apply: the data *is* held and *is* public regardless. Removing the index buys
**zero** privacy and destroys a real, self-sufficient on-chain feature.

The only genuine cost of enumeration is **gas/storage** — an efficiency tradeoff, not a privacy
principle. For a **public registry** (IP ownership, provenance), on-chain queryability *is* the
value proposition and is worth that cost. The contract must be the source of truth and usable
without any external indexer.

## Correction already applied

- **Removed** the offending bullet from `docs/engineering/contract-design-conventions.md` (§ Data
  minimization).
- **Kept** `docs/architecture/01-principles.md` §8 "Privacy is sovereignty" — it is correct and
  unrelated: it governs **private/sensitive** data (identities, PII, links → minimize, prefer zk),
  **not** queryability of public data.

## Corrected rule

- **Public data** (ownership, provenance, subscriptions, membership): on-chain enumeration is a
  feature. Keep it. The contract stands alone.
- **Private/sensitive data**: do not put it on-chain in the clear; minimize or use zk (§8).
- Enumeration is **never** a privacy decision. If enumeration is ever dropped, the only valid
  reason is a measured gas/DoS concern (e.g. an *unbounded vec the contract itself iterates in a
  state-changing path*) — and the fix is bounding/pagination, not deletion.

## Plan — audit each contract separately

Each contract gets its **own** document under `docs/audits/contracts/<Name>.md`. Do not batch
changes across contracts; one contract, one doc, one review.

| Priority | Contract | Why | Doc |
|---|---|---|---|
| **1 — urgent** | `MIP-Collections-ERC721` | In production, missing the expected royalties feature; foundational to the platform | `contracts/MIP-Collections-ERC721.md` ✅ created |
| 2 | `IP-Subscription` | Subscriber roster removed citing "data minimization" — likely a real feature stripped for no privacy gain | re-review pending |
| 2 | `IP-Time-Capsule` | `ERC721Enumerable` removed under the same reasoning | re-review pending |
| 2 | `IP-Club` | Cites the same reasoning — verify what was removed | re-review pending |
| 2 | `IP-Sponsorhip` | Cites the same reasoning — verify what was removed | re-review pending |
| 3 | All remaining `contracts/*` | Sweep for any other enumeration/roster removed on privacy grounds | pending |

### Method per contract

1. Identify any feature removed citing "data minimization / data not held cannot be compelled".
2. Classify the data: **public** (restore the feature) vs **genuinely private** (removal stands).
3. If a real gas/DoS concern exists, design bounding/pagination instead of deletion.
4. Record the decision in that contract's audit doc. Re-deploy only as part of that contract's own
   migration.

> Note: contracts already redeployed without the feature become **external/legacy** after their
> corrected redeploy — consistent with the platform's "new protocol; old collections become
> external" migration model. No legacy patching.
