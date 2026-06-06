# Mediolano Documentation — Vision Slice (Manifesto + Litepaper) — Design Spec

**Date:** 2026-06-06
**Status:** Draft for review.
**Repo:** `mediolano-core` (documentation only). Fully public once complete.
**Scope:** **Slice 1** of the Mediolano documentation program — the **Manifesto** and **Litepaper**.
The broader program (the rewrite of the legacy docs corpus) is recorded here as governing context;
only Slice 1 is specified for implementation.

---

## 1. Goal

Position **Mediolano OS** as **public-goods tokenization for the Integrity Web** through two
public documents: a bold **Manifesto** (the soul) and an accessible **Litepaper** (the on-ramp,
for everyone). Both are grounded in the [Integrity Web Axioms](../../architecture/00-axioms.md)
and consistent with the architecture (`00`–`09`).

---

## 2. The documentation program (governing context)

The legacy documentation lives in the cloned dapp at `mediolano-app/src/app/docs/` (17 topics, as
React TSX with prose embedded in presentational JSX). It is outdated and predates the current
foundation (e.g. the old `protocol` doc describes a single `IPCollection` contract and is
Starknet-centric). It is **source material to review, correct, and rewrite** — not to copy.

### Old → new mapping (whole corpus)

| Legacy doc | Treatment |
|---|---|
| Mediolano Protocol | Fold + redirect → `concepts/how-it-works`, links to `architecture/` (no contract docs yet) |
| IP Protection | Rewrite → `concepts/ip-protection` (align to `05`, axioms) |
| Programmable Licensing | Rewrite → `concepts/programmable-licensing` (align to `05`) |
| Public Goods | **Superseded by this slice** (Manifesto + Litepaper) and `09 Stewardship` |
| FAQ | Rewrite → `faq.md` |
| Security | Rewrite → `policy/security` (align to immutability, CROPS-Security) |
| Developers | Rewrite (light) → `guides/developers` (principle-level until contracts) |
| Permissionless Setup | Rewrite (light) → `guides/permissionless-setup` |
| DApp Guide | Rewrite → `guides/dapp-guide` (into core; marked as documenting the reference dapp) |
| User Guide | Rewrite → `guides/user-guide` (into core; marked as documenting the reference dapp) |
| Mediolano DAO | Rewrite → `governance/mediolano-dao` (reconcile with `09`) |
| Community Guidelines | Rewrite → `governance/community-guidelines` |
| Compliance Guidelines | Rewrite → `governance/compliance-guidelines` |
| DAO Constitution | ⚠ Review & flag → governing doc; align + surface changes for sign-off |
| Governance Charter | ⚠ Review & flag → governing doc; align + surface changes for sign-off |
| Terms of Use | ⚠ Review & flag → legal; align + flag for review |
| Privacy Policy | ⚠ Review & flag → legal; align to Privacy axiom (data minimization) + flag |

### Target information architecture

```
docs/
  manifesto.md            ← THIS SLICE
  litepaper.md            ← THIS SLICE
  architecture/00-09      ← done
  glossary.md             ← done
  concepts/               ← Slice 2
  guides/                 ← Slice 5 (incl. dapp-guide, user-guide)
  governance/             ← Slice 3 (incl. ⚠ constitution, charter)
  policy/                 ← Slice 4 (incl. ⚠ terms, privacy; + security)
  faq.md                  ← Slice 2
  README.md               ← updated as the hub
```

### Two governing principles for the whole rewrite

1. **Architecture stays canonical.** Concepts/guides are the accessible layer that links down to
   `00`–`09`; never a second, drifting source of truth.
2. **Sensitive docs are reviewed, not freely rewritten.** The four ⚠ governing/legal documents are
   aligned to the foundation with changes flagged for the user's sign-off.

### Sequencing

Slice 1 Vision → Slice 2 Concepts (+FAQ) → Slice 3 Governance → Slice 4 Policy/legal →
Slice 5 Guides. Each slice is its own spec → plan → implementation.

---

## 3. Slice 1 — artifacts & home

Two new documents, top-level in `docs/` so they are the front door, linked from `docs/README.md`:

```
docs/manifesto.md     # The bold declaration — the soul
docs/litepaper.md     # The accessible on-ramp — for everyone
```

Clean Markdown that renders well on GitHub and ports to a docs site later. No site tooling in this
slice.

---

## 4. `manifesto.md` — design

**Voice:** a bold cypherpunk declaration, matched to the axioms' register ("A Fine Art Declaration
of Digital Freedom"). Short, principled, quotable; readable in ~2 minutes and meant to be *felt*.

**Structure:**
- **Title + tagline:** *Mediolano — Public-goods tokenization for the Integrity Web.*
- **Preamble:** one defiant paragraph on why Mediolano exists (IP is the inheritance of human and
  machine culture; it must be free, durable, and owned by its creators).
- **Declarative stanzas**, each a short axiom-rooted truth (worn lightly — no inline citations):
  - *Creativity is integrity.* (Ax 09)
  - *Authorship is permanent.* (Ax 04, 01)
  - *No gatekeepers. No fees.* (Ax 03, 05)
  - *Privacy is sovereignty.* (Ax 06)
  - *For every intelligence — human to AI.* (Ax 08)
  - *Owned by no chain.* (Ax 07)
  - *A commons, forever.* (Ax 05, 10)
- **Closing call:** create, build on it, steward it.

**Length:** ~250–500 words. No roadmap, no timelines, no "Medialane."

---

## 5. `litepaper.md` — design

**Audience:** everyone — layered so a creator, a funder, and a developer each get what they need.
Each section opens with a plain-language line, then adds substance, then links to the architecture
for depth. Target ~1,500–2,500 words.

**Sections** (with the corrected source material each draws on):

1. **What Mediolano is** — one-liner + a paragraph. *(source: protocol intro, org README)*
2. **The problem** — IP today is fragile, gatekept, platform-locked, jurisdiction-bound. *(new)*
3. **The idea** — tokenize IP as a public good; durable, verifiable authorship for the Integrity
   Web. *(source: ip-protection, public-goods — corrected)*
4. **How it works** (plain) — immutable authorship records, content-addressed metadata,
   programmable licensing, the protocol-not-app model. → links `02`, `03`, `05`. *(source: protocol,
   programmable-licensing — corrected)*
5. **Why it's a public good** — zero-fee, neutral, immutable, forkable; CROPS in a sentence.
   → links `01`, `09`. *(source: public-goods — corrected)*
6. **For everyone, every intelligence** — human to AI; Berne-aligned across 180+ countries.
   → links `05`, `07`.
7. **Owned by no chain** — chain sovereignty / multichain in one accessible pass. → links `08`.
8. **How to take part** — use it, build on it, steward it (links: ip.mediolano.app, the repos,
   community).
9. **Go deeper** — architecture, axioms, glossary.

---

## 6. Authoring rules (Slice 1)

- **Defer to the axioms**; stay consistent with `00`–`09` (zero-fee, immutable, permissionless,
  universality, Berne, chain-sovereignty). No contradictions.
- **Present reality is allowed; promises are not.** Positioning copy may state what exists today in
  the conservative phrasing already used publicly ("powered on Starknet"), but makes **no roadmap or
  timeline promises** and does not reintroduce a "Starknet-now / others-later" framing — multichain
  is presented as the *principle* "owned by no chain" (`08`).
- **Stands fully alone** — no "Medialane" anywhere; centered on *public-goods tokenization for the
  Integrity Web*.
- **Manifesto stays poetic** (no citations in body); **Litepaper stays accessible** (plain-first,
  links for depth).

---

## 7. Out of scope (this slice)

- Slices 2–5 (concepts, governance, policy/legal, guides) and the FAQ.
- The four ⚠ governing/legal documents.
- Any docs-site tooling.
- Contract-level reference (contracts are a separate later effort).
- Publishing the repo public (happens when the foundation is judged complete).

---

## 8. Deferred / open

- Whether a rendered docs site (and which generator) is wanted — later.
- Exact handling of the ⚠ governing/legal docs — Slices 3–4, with user sign-off.
- A media/hero image for the manifesto (the org profile uses one) — optional, user-supplied.
