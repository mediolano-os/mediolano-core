# Mediolano Docs — Vision Slice (Manifesto + Litepaper) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Write the public **Manifesto** and **Litepaper** that position Mediolano OS as public-goods tokenization for the Integrity Web.

**Architecture:** Two top-level Markdown documents in `mediolano-core/docs/`, grounded in the [Integrity Web Axioms](../../architecture/00-axioms.md) and consistent with architecture `00`–`09`. The Manifesto is a bold, axiom-rooted declaration; the Litepaper is an accessible-to-everyone, layered on-ramp that links into the architecture for depth. Corrected content is mined from the legacy docs in `mediolano-app/src/app/docs/`.

**Tech Stack:** Markdown only. Source of truth for content & rules: `docs/superpowers/specs/2026-06-06-mediolano-docs-vision-design.md`.

**Working branch:** `feat/mediolano-docs-vision` (already created; the spec is committed there). Do NOT push.

---

## Conventions for every task

- **Voice:** Manifesto = bold, declarative, quotable, poetic (no inline citations). Litepaper = plain-language-first, then substance, then links for depth.
- **Forbidden (verification-gated):** never the string `medialane` (any case); no roadmap/timeline *promises* (`roadmap`, `coming soon`, `will launch`, `next quarter`, `by 202x`, `q1/q2/q3/q4 202x`). **Present reality is allowed** — e.g. "powered on Starknet" — but multichain is framed as the principle *"owned by no chain"* (`08`), never "Starknet now / others later".
- **Defer to the axioms; stay consistent with `00`–`09`** (zero-fee, immutable, permissionless, universality, Berne, chain-sovereignty).
- **Per-task verification gate** (run after each draft, before commit):

```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/<FILE>
```
Expected: **no output**.

---

## Task 1: `manifesto.md`

**Files:**
- Create: `docs/manifesto.md`

- [ ] **Step 1: Write the manifesto.** Bold declaration, ~250–500 words. Structure:
  - **Title + tagline:** `# Mediolano` / *Public-goods tokenization for the Integrity Web.*
  - **Preamble:** one defiant paragraph — IP is the inheritance of human and machine culture; it must be free to create, permanent once made, and owned by its creators, not by platforms.
  - **Declarative stanzas** (each a short heading + 1–3 punchy lines, axiom-rooted, worn lightly — no citations in the text):
    - *Creativity is integrity.* — knowledge, art, and invention tokenized as public goods; ideas free, their integrity preserved forever. (Ax 09)
    - *Authorship is permanent.* — every record tamper-proof, every action verifiable; what is proven is true. (Ax 04, 01)
    - *No gatekeepers. No fees.* — participation is permissionless; the primitives are a zero-fee commons. (Ax 03, 05)
    - *Privacy is sovereignty.* — prove without revealing; information belongs to its creator. (Ax 06)
    - *For every intelligence.* — humans, AI agents, and future intelligences, on equal terms. (Ax 08)
    - *Owned by no chain.* — verifiable trust is a role, not a place; identity and work survive any chain. (Ax 07)
    - *A commons, forever.* — infrastructure that belongs to everyone, the trust backbone of digital civilization. (Ax 05, 10)
  - **Closing call:** create on it, build on it, steward it. Optional one-line link to the [Litepaper](litepaper.md) and [Axioms](architecture/00-axioms.md).

- [ ] **Step 2: Verify.** Run the gate for `manifesto.md`. Confirm length is ~250–500 words:

```bash
cd /Users/kalamaha/dev/mediolano-core && wc -w docs/manifesto.md
```
Expected: roughly 250–500 words; gate output empty.

- [ ] **Step 3: Commit.**

```bash
git add docs/manifesto.md
git commit -m "docs: Mediolano manifesto — public-goods tokenization for the Integrity Web"
```

---

## Task 2: `litepaper.md`

**Files:**
- Create: `docs/litepaper.md`
- Read (source material, do not copy — correct & rewrite): `mediolano-app/src/app/docs/protocol/ProtocolContent.tsx`, `.../public-goods/PublicGoodsContent.tsx`, `.../ip-protection/IPProtectionContent.tsx`, `.../programmable-licensing/ProgrammableLicensingContent.tsx`, `.../faq/FAQContent.tsx`

- [ ] **Step 1: Mine the legacy sources.** Read the five files above; extract accurate, reusable points (what Mediolano is, the IP problem, public-goods framing, how protection/licensing works) and discard anything that conflicts with the current foundation (single-`IPCollection` framing, Starknet-as-permanent-home, any fee/▲outdated claims).

- [ ] **Step 2: Write the litepaper.** ~1,500–2,500 words, accessible to everyone, layered (plain line → substance → depth link). Sections:
  1. **What Mediolano is** — one-liner + a paragraph.
  2. **The problem** — IP today is fragile, gatekept, platform-locked, jurisdiction-bound.
  3. **The idea** — tokenize IP as a public good; durable, verifiable authorship for the Integrity Web.
  4. **How it works** — immutable authorship records, content-addressed metadata, programmable licensing, protocol-not-app. Link: [02](architecture/02-core-model.md), [03](architecture/03-protocol-and-apps.md), [05](architecture/05-licensing-and-authorship.md).
  5. **Why it's a public good** — zero-fee, neutral, immutable, forkable; CROPS in a sentence. Link: [01](architecture/01-principles.md), [09](architecture/09-stewardship.md).
  6. **For everyone, every intelligence** — human to AI; Berne-aligned across 180+ countries. Link: [05](architecture/05-licensing-and-authorship.md), [07](architecture/07-identity.md).
  7. **Owned by no chain** — chain sovereignty / multichain, one accessible pass. Link: [08](architecture/08-chain-sovereignty.md).
  8. **How to take part** — use it (<https://ip.mediolano.app>), build on it (the public repos), steward it (community <https://t.me/integrityweb>).
  9. **Go deeper** — links to [the architecture](architecture/README.md), [axioms](architecture/00-axioms.md), [glossary](glossary.md).

- [ ] **Step 3: Verify.** Run the gate for `litepaper.md`. Confirm every architecture link target exists and word count is in range:

```bash
cd /Users/kalamaha/dev/mediolano-core
ls architecture/02-core-model.md architecture/03-protocol-and-apps.md architecture/05-licensing-and-authorship.md architecture/01-principles.md architecture/09-stewardship.md architecture/07-identity.md architecture/08-chain-sovereignty.md architecture/00-axioms.md architecture/README.md glossary.md
wc -w docs/litepaper.md
```
Expected: all files listed (no "No such file"); ~1,500–2,500 words; gate output empty.

- [ ] **Step 4: Commit.**

```bash
git add docs/litepaper.md
git commit -m "docs: Mediolano litepaper — accessible overview of the public-goods substrate"
```

---

## Task 3: Surface both docs in the docs hub

**Files:**
- Modify: `docs/README.md`

- [ ] **Step 1: Edit `docs/README.md`.** Add a short top section, directly under the intro paragraph and before "Reading order", that points to the two new documents as the front door:

```markdown
## Start here

- **[Manifesto](manifesto.md)** — why Mediolano exists, in brief.
- **[Litepaper](litepaper.md)** — an accessible overview of the protocol, for everyone.
```

- [ ] **Step 2: Verify.** Run the gate for `README.md`; confirm both links present.

```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/README.md
grep -c 'manifesto.md\|litepaper.md' docs/README.md
```
Expected: gate empty; count ≥ 2.

- [ ] **Step 3: Commit.**

```bash
git add docs/README.md
git commit -m "docs: surface manifesto + litepaper in the docs hub"
```

---

## Task 4: Final consistency pass

**Files:**
- Touch as needed: `docs/manifesto.md`, `docs/litepaper.md`, `docs/README.md`

- [ ] **Step 1: Repo-wide gate over the new docs.**

```bash
cd /Users/kalamaha/dev/mediolano-core
grep -rniE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/manifesto.md docs/litepaper.md docs/README.md
```
Expected: no output. Fix any hit.

- [ ] **Step 2: Axiom/architecture consistency check.** Reread the manifesto stanzas and litepaper claims against `00`–`09`; confirm no contradiction (zero-fee, immutable, permissionless, universality, Berne, chain-sovereignty) and that multichain is framed as "owned by no chain" (no "Starknet-first" sequencing).

- [ ] **Step 3: Commit any fixes.**

```bash
git add -A docs/
git commit -m "docs: final consistency pass on vision slice" || echo "nothing to fix"
```

---

## Self-Review (completed during plan authoring)

- **Spec coverage:** Manifesto (spec §4) → Task 1; Litepaper (spec §5, incl. source mining and architecture links) → Task 2; surfacing in the hub (spec §3 IA, README as hub) → Task 3; authoring rules (spec §6) enforced by the per-task gate + Task 4. The program-context (spec §2) is recorded, not implemented this slice — correct.
- **Placeholder scan:** no TBD/TODO; each task carries concrete structure, content points, sources, exact commands.
- **Consistency:** the gate pattern, section list, and architecture link targets are identical across tasks and match the spec; link targets verified to exist in Task 2/3.
