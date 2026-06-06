# Mediolano Documentation — Governance Slice — Design Spec

**Date:** 2026-06-06
**Status:** Draft for review.
**Repo:** `mediolano-core` (documentation only). Fully public once complete.
**Scope:** **Slice 3** of the Mediolano documentation program — governance docs, including the two
governing instruments handled as ratification-pending drafts, plus a light amendment to
`09-stewardship`. Governing program context:
`2026-06-06-mediolano-docs-vision-design.md`.

---

## 1. Goal

Establish Mediolano's public governance documentation — what the DAO is, how it governs, how the
community participates, and the (draft) governing instruments — reconciled with the current
foundation (`00`–`09`) and corrected against the legacy docs.

---

## 2. Decisions locked in brainstorming

- **Treasury model:** the **protocol primitives stay strictly zero-fee** (hard invariant). The
  **DAO sustains itself off-protocol** — optional premium services / app-layer offerings, grants,
  donations — **never by metering the primitives**. This requires a light amendment to
  `09-stewardship` clarifying the protocol-vs-DAO funding line.
- **Governance machinery is current — document as-is:** **MIP token** membership; **Snapshot**
  platform; **1 token = 1 vote**; delegation; minimum holding to submit proposals; timelocked
  on-chain execution; working groups / SubDAOs; AI-agent / autonomous-intelligence participation.
  (Do **not** invent a governance-token contract address — describe MIP as the governance token and
  leave any address for the user to supply.)
- **Constitution + Governance Charter** ship as **aligned drafts marked "pending ratification,"**
  each with a visible **"Changes from the legacy version"** box flagging every substantive change.
- **compliance-guidelines** is **informational**, with a "general information, not legal advice"
  note; uncertain points flagged, not asserted.

---

## 3. Artifacts & home

```
docs/governance/
  mediolano-dao.md          # accessible overview: mission, governance model, treasury
  community-guidelines.md   # rewrite (accessible)
  compliance-guidelines.md  # rewrite (informational; not legal advice)
  constitution.md           # ⚠ aligned DRAFT — pending ratification
  governance-charter.md     # ⚠ aligned DRAFT — pending ratification
```
Plus:
- **Amend** `docs/architecture/09-stewardship.md` (protocol-vs-DAO funding clarification).
- Add a **Governance** section to `docs/README.md` (hub) and a line to root `README.md`.

Legacy sources (review & rewrite, do not copy): `mediolano-app/src/app/docs/{mediolano-dao,
dao-constitution,governance-charter,community-guidelines,compliance-guidelines}/`.

---

## 4. The `09-stewardship` amendment

Keep the existing zero-fee invariant text intact ("no fees in the immutable primitives, no
extraction from the substrate"; the "rules out" list). **Add** a short clarifying paragraph
(timeless — no temporal framing, honoring the architecture authoring gate):

- The protocol primitives are zero-fee and take nothing; this is distinct from how the **DAO**
  sustains *itself*.
- The DAO may fund its stewardship **off-protocol** — optional premium services, grants, and
  donations — and recycle surplus into public goods. It must **never** meter, tax, or extract from
  the primitives to do so.
- This preserves "governance without extraction *from the substrate*" while allowing the DAO to be
  sustainable.

The architecture gate (`today|currently|year-N|v1|…`) still applies to this file — the amendment
must read as a timeless principle.

---

## 5. Per-document design

All docs link to the architecture they derive from. Accessible docs use the layered voice; the two
instruments use a formal articled voice.

### `governance/mediolano-dao.md` (accessible)
Mission and governance model: the DAO as steward of a zero-fee public good; **off-protocol
funding** model (premium services / grants / donations → public goods); membership and voting
(MIP token, Snapshot, 1-token-1-vote, delegation); working groups / SubDAOs; AI-agent
participation. Links `09`, `01`, `00`.

### `governance/community-guidelines.md` (accessible)
Community norms aligned to the axioms (permissionless participation, respect for all intelligences,
integrity, contribution). Corrected/condensed from legacy. Links `00`, `09`.

### `governance/compliance-guidelines.md` (informational)
Opens with **"general information, not legal advice."** Covers the substrate's compliance posture
at a principled level (non-custodial, neutral infrastructure; Berne-aligned authorship records;
the securities-regulation topic framed cautiously, asserting no legal status). Uncertain/legal
specifics flagged for review. Links `05`, `09`.

### `governance/constitution.md` (⚠ DRAFT — pending ratification)
Formal articled draft. Opens with a **Status box**: *"Draft pending ratification by the Mediolano
DAO — not yet enacted,"* then a **"Changes from the legacy version"** list. Articles cover: name &
purpose (public goods for creators/IP, all intelligences); membership (MIP token; individuals,
organizations, DAOs, AI agents); rights & responsibilities; governance process (Snapshot, simple
majority, delegation, min-holding-to-propose, timelocked execution); working groups / SubDAOs;
**treasury (realigned: off-protocol funding; protocol primitives zero-fee)**; amendment process.
**Headline flagged change:** treasury realignment + zero-fee reconciliation; minor:
Starknet→"powered on Starknet, owned by no chain" softening. Links `09`, `00`.

### `governance/governance-charter.md` (⚠ DRAFT — pending ratification)
Formal draft of operational governance rules. Same Status box + changes list. Covers: governing
principles (sovereignty, transparency, innovation, inclusivity); proposal lifecycle; voting &
delegation; thresholds; timelocked execution; use of funds (protocol development, contributor
compensation, public-goods funding — all **off-protocol** sourced). Links `09`,
`governance/constitution.md`.

---

## 6. Authoring rules (this slice)

- Defer to the axioms; stay consistent with `00`–`09` (as amended).
- Gate per doc: never `medialane`; no roadmap/timeline promises. Present-reality facts allowed
  (`Snapshot`, `MIP token`, `powered on Starknet`).
- The two ⚠ instruments must carry the Status box + "Changes from the legacy version" list.
- Do not assert a governance-token contract address or any legal status; flag unknowns.
- All inter-doc links resolve.

---

## 7. Out of scope (this slice)

- Slice 4 (policy/legal: terms of use, privacy policy, security) and Slice 5 (guides).
- Enacting/ratifying the constitution or charter — they ship as drafts only.
- Inventing token addresses, legal entities, or jurisdictional claims.
- Docs-site tooling; publishing the repo public.

---

## 8. Deferred / open

- Governance-token contract address and any on-chain governance contracts — user-supplied later.
- Final legal review of compliance-guidelines and the instruments — outside this docs effort.
- Ratification of the constitution/charter — a DAO action, not a docs action.
