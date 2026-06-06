# Mediolano Documentation — Concepts Slice — Design Spec

**Date:** 2026-06-06
**Status:** Draft for review.
**Repo:** `mediolano-core` (documentation only). Fully public once complete.
**Scope:** **Slice 2** of the Mediolano documentation program — accessible **concept explainers**
plus the **FAQ**. Governing program context lives in
`2026-06-06-mediolano-docs-vision-design.md` (old→new mapping, IA, sequencing, rules).

---

## 1. Goal

Rewrite the most outdated legacy conceptual docs into accessible explainers that sit between the
[Litepaper](../../litepaper.md) and the architecture (`00`–`09`) — correct against the current
foundation, link down for depth, and never become a second source of truth.

Covers four documents: `concepts/how-it-works`, `concepts/ip-protection`,
`concepts/programmable-licensing`, and a top-level `faq.md`.

---

## 2. Context: legacy sources & required corrections

Source material in `mediolano-app/src/app/docs/` (review & rewrite — do not copy):

- `protocol/ProtocolContent.tsx` — **most outdated.** Describes **upgradeable contracts with admin
  access control**, a single `IPCollection` contract, and Starknet-only interaction. **Must be
  corrected** to: immutable primitives (no admin/owner/upgrade — `01 §3`), many service modules
  (`06`), chains-as-peers (`08`).
- `ip-protection/IPProtectionContent.tsx` — has good Berne specifics (automatic protection on
  fixation, no registration, national treatment, independence of rights, TRIPS/WTO reach;
  "verifiable stack, no backdoors").
- `programmable-licensing/ProgrammableLicensingContent.tsx` — largely aligned & rich: immutable
  license proof committed at mint, IPFS/Arweave permanence, CC compatibility, remix/ShareAlike
  propagation, AI agents verifying rights. **Correct** Starknet-specific bits (named marketplaces,
  L1/L2 "bridging") to neutral / chain-sovereign framing.
- `faq/FAQContent.tsx` — question seeds (file types, edit-after-mint, cost, audits).

---

## 3. Artifacts & home

```
docs/
  concepts/
    how-it-works.md
    ip-protection.md
    programmable-licensing.md
  faq.md
```
Both READMEs updated: add a **Concepts** group and a **FAQ** link to `docs/README.md` (the hub)
and to the root `README.md` documentation list.

---

## 4. Per-document design

Every doc: layered (plain-language line → substance → `→ Go deeper` architecture links); same
voice as the Litepaper; opens with the standard `**Authority:** the axioms govern…` line is **not**
required for these accessible docs, but each must link to the architecture doc(s) it derives from.

### `concepts/how-it-works.md`
The fuller walkthrough (supersedes the legacy `protocol` doc). Differentiated from Litepaper §4 by
following an IP asset's **lifecycle**:
1. **Tokenize** — mint an authorship record.
2. **Protect** — immutable, content-addressed metadata; provenance on-chain.
3. **License** — programmable, metadata-first terms.
4. **Use & compose** — services (transfer, trade, remix, access, revenue share…).
5. **Protocol, not app** — chain is truth; apps present, never authorize; immutable & zero-fee.
Corrections: no upgradeability/admin; not a single contract; chains are peers.
Links: [02](../architecture/02-core-model.md), [03](../architecture/03-protocol-and-apps.md),
[05](../architecture/05-licensing-and-authorship.md), [06](../architecture/06-service-model.md).

### `concepts/ip-protection.md`
"How does Mediolano protect IP?" Covers: what protection means here (durable, independently
verifiable authorship **evidence**, not legal adjudication); how content-addressing makes records
tamper-proof; **Berne alignment** (automatic on fixation, no registration, national treatment,
independence of rights; TRIPS/WTO reach); the verifiable-stack / no-backdoors point.
Links: [05](../architecture/05-licensing-and-authorship.md),
[07](../architecture/07-identity.md), [00](../architecture/00-axioms.md).

### `concepts/programmable-licensing.md`
Covers: licenses as portable metadata; immutable license proof committed at mint; **the creator
chooses from CC-compatible options — no protocol-wide default is pinned**; soft-enforced by default
+ selective on-chain enforcement; readable by wallets/marketplaces/indexers/agents;
remix/derivative & ShareAlike propagation; AI agents verifying rights autonomously. Corrections:
replace named Starknet marketplaces and L1/L2 "bridging" with neutral, chain-sovereign framing.
Links: [05](../architecture/05-licensing-and-authorship.md),
[04](../architecture/04-interoperability.md), [06](../architecture/06-service-model.md).

### `docs/faq.md`
Corrected Q&A, grouped. Question set (answers aligned to the foundation):
- **What is Mediolano?**
- **What can I tokenize?** (broad range of works)
- **Does it cost anything?** (zero-fee protocol; app/network costs are separate)
- **Can I edit my IP after minting?** (no — records are immutable; that is the point)
- **Who owns my IP?** (the creator; the protocol is non-custodial)
- **How is my authorship protected?** (durable, verifiable records; Berne alignment)
- **Can I choose a license?** (yes — programmable, CC-compatible; creator chooses)
- **Does my asset work on other wallets and marketplaces?** (yes — standard interfaces)
- **Can AI agents use Mediolano?** (yes — first-class, equal terms)
- **What chains does it run on?** (powered on Starknet; designed owned-by-no-chain)
- **Are the contracts immutable and audited?** (immutable by design; audits are public)
- **Is it open source?** (yes — neutral, forkable public infrastructure)
- Closing: links to Litepaper, architecture, glossary.

---

## 5. Default license stance

The docs present licensing as **"the creator chooses from CC-compatible options"** and **do not
pin a protocol-wide default** — consistent with the architecture (which pins none) and with
permissionless/neutral framing.

---

## 6. Authoring rules (same as the program)

- Defer to the axioms; stay consistent with `00`–`09`.
- Verification gate per doc: never `medialane`; no roadmap/timeline promises
  (`roadmap`, `coming soon`, `will launch`, `next quarter`, `by 202x`, `qN 202x`). Present reality
  allowed ("powered on Starknet"); multichain framed as "owned by no chain".
- Accessible layered voice; architecture stays canonical (link down, don't restate as truth).
- All inter-doc links must resolve.

---

## 7. Out of scope (this slice)

- Slices 3–5 (governance, policy/legal, guides) and the four ⚠ governing/legal docs.
- Contract-level reference (contracts are a separate later effort).
- Any docs-site tooling.
- Publishing the repo public.

---

## 8. Deferred / open

- A `concepts/README.md` index — optional; can fold into the docs hub instead (default: hub only).
- The exact public audits index/location — surfaced when audits are published.
