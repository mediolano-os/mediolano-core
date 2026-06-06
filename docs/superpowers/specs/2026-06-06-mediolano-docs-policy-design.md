# Mediolano Documentation — Policy / Legal Slice — Design Spec

**Date:** 2026-06-06
**Status:** Draft for review.
**Repo:** `mediolano-core` (documentation only). Fully public once complete.
**Scope:** **Slice 4** of the documentation program — Terms of Use, Privacy Policy (both legal
drafts), and Security. Governing program context:
`2026-06-06-mediolano-docs-vision-design.md`.

---

## 1. Goal

Rewrite the legacy policy/legal docs against the current foundation: Terms of Use and Privacy
Policy as drafts pending legal review; Security as an accurate, non-custodial risk/posture doc.

---

## 2. Decisions locked in brainstorming

- **Terms + Privacy ship as drafts pending legal review** — opening box: *"Draft — pending legal
  review; general information, not legal advice; not yet in force,"* plus a **"Changes from the
  legacy version"** list. (All legal docs will go through a legal audit.)
- **Security is a straightforward rewrite** with a light informational/risk note (not a ⚠ legal
  instrument).
- **Privacy contact:** keep `mediolanoapp@gmail.com`, marked provisional/pending review.
- **Corrections** (below) applied across all three.

---

## 3. Corrections to apply

- **Berne overclaim → evidence framing.** Tokenization produces *verifiable authorship evidence
  aligned with the Berne Convention*; recognition flows from authorship of the underlying work,
  not from minting. Standardize to **"180+ Berne member states"** (exact figure flagged for legal
  review; legacy said 173).
- **Non-custodial (security).** Reframe "user funds at risk" → risk to the user's **own
  self-custodied assets**; Mediolano holds nothing and can freeze nothing.
- **Privacy = data minimization (Axiom 06).** Keep/strengthen: no default cookies, trackers, or
  behavioral analytics; minimal data collection; prove-without-revealing. **Fold cookie handling
  into the privacy policy**; drop the dangling separate "Cookie Policy" reference.
- **Chain framing.** "powered on Starknet" (present reality); durability framed as *owned by no
  chain*; keep the factual Starknet→Ethereum settlement note light, not as a permanence claim.
- **Governance linkage.** Amendment/governance handled via the DAO — link the governance docs.

---

## 4. Artifacts & home

```
docs/policy/
  terms-of-use.md      # ⚠ DRAFT — pending legal review
  privacy-policy.md    # ⚠ DRAFT — pending legal review
  security.md          # rewrite
```
Add a **Policy** section to `docs/README.md` (hub) and a line to root `README.md`.

Legacy sources (review & rewrite): `mediolano-app/src/app/docs/{terms-of-use,privacy-policy,
security}/`.

---

## 5. Per-document design

All link to the architecture/governance they derive from. Same docs gate (no `medialane`; no
roadmap/timeline promises; present-reality like "powered on Starknet" allowed).

### `policy/terms-of-use.md` (⚠ DRAFT — pending legal review)
Status box + changes list, then sections:
- **Acceptance** — by using the protocol/apps you agree; terms amendable through DAO governance.
- **What Mediolano is** — permissionless, open-source protocol; non-custodial; zero-fee primitives;
  Berne-aligned authorship *evidence* (corrected from the recognition overclaim).
- **User responsibilities** — lawful use; you control your own assets/keys; you are responsible for
  what you tokenize and for your rights to it.
- **Intellectual property** — authorship/ownership records are evidence; **jurisdictional
  enforcement remains the creator's responsibility**; Berne term (50–70 years, by jurisdiction).
- **No custody / no fees** — the protocol holds nothing and charges nothing at the primitive layer.
- **Disclaimers & risk** — software/contract risk; "as is"; pointer to Security.
- **Governance & amendment** — via Mediolano DAO (link governance).
- **Changes from legacy:** Berne overclaim softened; count standardized; chain framing aligned;
  zero-fee/non-custodial made explicit.
Links: `[Licensing & Authorship](../architecture/05-licensing-and-authorship.md)`,
`[Mediolano DAO](../governance/mediolano-dao.md)`, `[Security](security.md)`.

### `policy/privacy-policy.md` (⚠ DRAFT — pending legal review)
Status box + changes list, then:
- **Our stance** — privacy as a right (Axiom 06); data minimization; prove-without-revealing.
- **What we collect** — minimal; **no default cookies, trackers, or behavioral analytics.**
- **On-chain data** — transactions are public by nature of blockchains; authorship/ownership live
  on-chain and are not private; users should understand this.
- **Cookies** — folded in: the dapp avoids cookies and similar technologies (no separate Cookie
  Policy doc).
- **Your control** — non-custodial; you hold your keys and data.
- **Contact** — `mediolanoapp@gmail.com` (provisional, pending legal review).
- **Changes from legacy:** dropped dangling Cookie Policy reference; aligned to data-minimization
  axiom; chain framing.
Links: `[Chain Sovereignty](../architecture/08-chain-sovereignty.md)`,
`[Stewardship](../architecture/09-stewardship.md)`.

### `policy/security.md` (rewrite)
- **Security posture** — immutable primitives (no admin/owner/upgrade); audits; verifiable stack;
  CROPS-Security.
- **Non-custodial risk framing** — risk is to the user's **own self-custodied assets**; Mediolano
  holds nothing and can freeze nothing.
- **Inherent risks** — smart-contract and underlying-network risk (Starknet/Ethereum); "use
  caution"; not financial advice.
- **Responsible disclosure** — a brief note inviting security reports (channel flagged/provisional).
Links: `[Principles](../architecture/01-principles.md)`,
`[Chain Sovereignty](../architecture/08-chain-sovereignty.md)`.

---

## 6. Authoring rules

- Defer to the axioms; consistent with `00`–`09` and the governance slice.
- Docs gate per file; the two ⚠ drafts carry the Status box + "Changes from the legacy version".
- Assert no legal status, no jurisdiction/legal entity, no token address; flag unknowns.
- All inter-doc links resolve.

---

## 7. Out of scope

- Slice 5 (guides).
- Enacting the legal terms; legal review itself (separate, by counsel).
- Inventing jurisdictions, legal entities, or a token address.
- Docs-site tooling; publishing the repo public.

---

## 8. Deferred / open

- Final legal review of Terms + Privacy (by counsel) and a confirmed privacy/security contact.
- Exact Berne member-state count — confirmed at legal review.
- A dedicated security disclosure channel/address — user-supplied later.
