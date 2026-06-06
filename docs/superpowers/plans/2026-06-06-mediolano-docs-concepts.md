# Mediolano Docs — Concepts Slice Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Write the accessible concept explainers (`how-it-works`, `ip-protection`, `programmable-licensing`) and the `faq`, correcting the outdated legacy docs against the current foundation.

**Architecture:** Four Markdown docs in `mediolano-core` — three under `docs/concepts/`, one at `docs/faq.md` — layered (plain line → substance → architecture links), consistent with the Litepaper voice, with the architecture (`00`–`09`) as the canonical source they link down to.

**Tech Stack:** Markdown only. Source of truth: `docs/superpowers/specs/2026-06-06-mediolano-docs-concepts-design.md`. Legacy source material: `mediolano-app/src/app/docs/`.

**Working branch:** `feat/mediolano-docs-concepts` (already created; spec committed there). Do NOT push.

---

## Conventions for every task

- **Voice:** accessible, layered (plain-language first line, then substance, then `→ Go deeper:` architecture links). Match the Litepaper register.
- **Architecture stays canonical:** link down to `00`–`09`; never restate architecture as a competing source of truth.
- **Default license:** present licensing as "the creator chooses from CC-compatible options"; **do not pin a protocol-wide default.**
- **Forbidden (verification-gated):** never `medialane` (any case); no roadmap/timeline promises (`roadmap`, `coming soon`, `will launch`, `next quarter`, `by 202x`, `qN 202x`). Present reality allowed ("powered on Starknet"); multichain framed as "owned by no chain".
- **Per-task gate** (run after each draft, before commit):

```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/<FILE>
```
Expected: no output.

- **Link convention:** files in `docs/concepts/` link to architecture as `../architecture/NN-*.md`, to glossary as `../glossary.md`, to litepaper as `../litepaper.md`. Files in `docs/` (faq.md) link as `architecture/NN-*.md`, `glossary.md`, `litepaper.md`.

---

## Task 1: `concepts/how-it-works.md`

**Files:**
- Create: `docs/concepts/how-it-works.md`
- Read (correct, don't copy): `mediolano-app/src/app/docs/protocol/ProtocolContent.tsx`

- [ ] **Step 1: Read the legacy `protocol` doc** and note what to correct: upgradeable contracts, admin access control, single `IPCollection`, Starknet-only interaction — all replaced per the foundation.

- [ ] **Step 2: Write the doc.** A lifecycle walkthrough of an IP asset on Mediolano, accessible and layered. Sections:
  1. **Intro** — one plain paragraph: how a work becomes a permanent, usable on-chain asset.
  2. **Tokenize** — mint an authorship record (who/what/when).
  3. **Protect** — immutable, content-addressed metadata (IPFS/Arweave); provenance on-chain.
  4. **License** — programmable, metadata-first terms that travel with the asset.
  5. **Use & compose** — services: transfer, trade, remix, access, revenue share.
  6. **Protocol, not app** — the chain is the source of truth; apps present but never authorize; the primitives are immutable and zero-fee.
  - **Corrections to honor:** no upgradeability/admin; not a single contract (many service modules); chains are peers (not Starknet-only).
  - **Links:** `[Core Model](../architecture/02-core-model.md)`, `[Protocol & Applications](../architecture/03-protocol-and-apps.md)`, `[Licensing & Authorship](../architecture/05-licensing-and-authorship.md)`, `[Service Model](../architecture/06-service-model.md)`.

- [ ] **Step 3: Verify.** Run the gate for `concepts/how-it-works.md`; confirm link targets exist:

```bash
cd /Users/kalamaha/dev/mediolano-core
for t in 02-core-model 03-protocol-and-apps 05-licensing-and-authorship 06-service-model; do [ -f "docs/architecture/$t.md" ] || echo "MISSING $t"; done
grep -niE 'upgrade|admin|owner' docs/concepts/how-it-works.md || echo "  (no stale upgrade/admin/owner language)"
```
Expected: no MISSING; review any upgrade/admin/owner hit to ensure it is a *negation* (e.g. "no admin"), not a stale claim.

- [ ] **Step 4: Commit.**

```bash
git add docs/concepts/how-it-works.md
git commit -m "docs(concepts): how Mediolano works — IP asset lifecycle"
```

---

## Task 2: `concepts/ip-protection.md`

**Files:**
- Create: `docs/concepts/ip-protection.md`
- Read (mine Berne specifics): `mediolano-app/src/app/docs/ip-protection/IPProtectionContent.tsx`

- [ ] **Step 1: Write the doc.** "How does Mediolano protect IP?" Accessible, layered. Cover:
  - **What protection means here** — durable, independently verifiable authorship *evidence*, not legal adjudication; the protocol records, courts/jurisdictions adjudicate.
  - **Why it's tamper-proof** — content-addressed metadata (the reference is the integrity check) + on-chain provenance.
  - **Berne alignment** — automatic protection the moment a work is fixed; no registration required; national treatment (recognized across member states); independence of rights; reach via TRIPS/WTO (180+ countries). Link <https://en.wikipedia.org/wiki/Berne_Convention>.
  - **A verifiable stack** — the whole record is checkable; no hidden backdoors.
  - **Links:** `[Licensing & Authorship](../architecture/05-licensing-and-authorship.md)`, `[Identity](../architecture/07-identity.md)`, `[Axioms](../architecture/00-axioms.md)`.

- [ ] **Step 2: Verify.** Run the gate for `concepts/ip-protection.md`; confirm Berne points present and link targets exist:

```bash
cd /Users/kalamaha/dev/mediolano-core
for t in 05-licensing-and-authorship 07-identity 00-axioms; do [ -f "docs/architecture/$t.md" ] || echo "MISSING $t"; done
grep -ci 'berne' docs/concepts/ip-protection.md
```
Expected: no MISSING; berne count ≥ 1; gate empty.

- [ ] **Step 3: Commit.**

```bash
git add docs/concepts/ip-protection.md
git commit -m "docs(concepts): how Mediolano protects IP — Berne-aligned, verifiable"
```

---

## Task 3: `concepts/programmable-licensing.md`

**Files:**
- Create: `docs/concepts/programmable-licensing.md`
- Read (mine, correct Starknet-specifics): `mediolano-app/src/app/docs/programmable-licensing/ProgrammableLicensingContent.tsx`

- [ ] **Step 1: Write the doc.** Accessible, layered. Cover:
  - **Licenses as portable metadata** — encoded as standard attributes that travel with the asset.
  - **Immutable license proof at mint** — the license terms are committed at creation and cannot be silently changed.
  - **Creator chooses; CC-compatible** — present CC compatibility (e.g. CC0, CC BY, CC BY-SA) as options the creator selects; **do not pin a protocol-wide default.**
  - **Soft-enforced by default, selective on-chain enforcement** — declared terms; contracts enforce only what a specific service implements.
  - **Interoperable** — readable by wallets, marketplaces, indexers, and agents (use neutral phrasing — no named marketplaces, no L1/L2 "bridging"; frame portability as "owned by no chain").
  - **Remix & derivatives** — ShareAlike propagation, attribution preserved, commercial limits inherited.
  - **AI agents** — machine-readable terms let agents verify rights before using content.
  - **Links:** `[Licensing & Authorship](../architecture/05-licensing-and-authorship.md)`, `[Interoperability](../architecture/04-interoperability.md)`, `[Service Model](../architecture/06-service-model.md)`.

- [ ] **Step 2: Verify.** Run the gate for `concepts/programmable-licensing.md`; confirm no Starknet-specific marketplace/bridging language and link targets exist:

```bash
cd /Users/kalamaha/dev/mediolano-core
for t in 05-licensing-and-authorship 04-interoperability 06-service-model; do [ -f "docs/architecture/$t.md" ] || echo "MISSING $t"; done
grep -niE 'element|flex|bridg' docs/concepts/programmable-licensing.md || echo "  (no named-marketplace / bridging language)"
```
Expected: no MISSING; no element/flex/bridging hits; gate empty.

- [ ] **Step 3: Commit.**

```bash
git add docs/concepts/programmable-licensing.md
git commit -m "docs(concepts): programmable licensing — portable, CC-compatible, agent-readable"
```

---

## Task 4: `faq.md`

**Files:**
- Create: `docs/faq.md`
- Read (seeds): `mediolano-app/src/app/docs/faq/FAQContent.tsx`

- [ ] **Step 1: Write the doc.** A grouped Q&A; each answer aligned to the foundation, 1–4 sentences. Questions:
  - **What is Mediolano?**
  - **What can I tokenize?** (broad range of works)
  - **Does it cost anything?** (zero-fee protocol; app/network costs are separate)
  - **Can I edit my IP after minting?** (no — records are immutable; that is the point)
  - **Who owns my IP?** (the creator; the protocol is non-custodial)
  - **How is my authorship protected?** (durable verifiable records; Berne alignment)
  - **Can I choose a license?** (yes — programmable, CC-compatible; creator chooses)
  - **Does my asset work on other wallets and marketplaces?** (yes — standard interfaces)
  - **Can AI agents use Mediolano?** (yes — first-class, equal terms)
  - **What chains does it run on?** (powered on Starknet; designed owned-by-no-chain)
  - **Are the contracts immutable and audited?** (immutable by design; audits are public)
  - **Is it open source?** (yes — neutral, forkable public infrastructure)
  - Closing: links to `[Litepaper](litepaper.md)`, `[architecture](README.md)`, `[glossary](glossary.md)`.

- [ ] **Step 2: Verify.** Run the gate for `faq.md`; confirm question count and link targets:

```bash
cd /Users/kalamaha/dev/mediolano-core
grep -c '^###\|^##' docs/faq.md
for t in litepaper.md README.md glossary.md; do [ -f "docs/$t" ] || echo "MISSING $t"; done
```
Expected: ≥ 12 question headings; no MISSING; gate empty.

- [ ] **Step 3: Commit.**

```bash
git add docs/faq.md
git commit -m "docs: FAQ — corrected answers aligned to the foundation"
```

---

## Task 5: Surface Concepts + FAQ in both READMEs

**Files:**
- Modify: `docs/README.md`
- Modify: `README.md`

- [ ] **Step 1: Edit `docs/README.md`.** After the architecture "Reading order" table and before "Supporting reference" (or alongside it), add:

```markdown
## Concepts

Accessible explainers that link into the architecture for depth.

- [How Mediolano works](concepts/how-it-works.md) — the lifecycle of an IP asset.
- [How Mediolano protects IP](concepts/ip-protection.md) — Berne-aligned, verifiable authorship.
- [Programmable licensing](concepts/programmable-licensing.md) — portable, CC-compatible rights.
- [FAQ](faq.md) — common questions.
```

- [ ] **Step 2: Edit root `README.md`.** In the "Documentation" list, add a line after the Architecture entry:

```markdown
- **[Concepts & FAQ](docs/README.md#concepts)** — accessible explainers and common questions.
```

- [ ] **Step 3: Verify.** Run the gate over both READMEs; confirm the new links present.

```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/README.md README.md
grep -c 'concepts/how-it-works.md\|faq.md' docs/README.md
```
Expected: gate empty; count ≥ 2.

- [ ] **Step 4: Commit.**

```bash
git add docs/README.md README.md
git commit -m "docs: surface Concepts + FAQ in the docs hub and root README"
```

---

## Task 6: Final consistency pass

**Files:**
- Touch as needed: `docs/concepts/*.md`, `docs/faq.md`, `docs/README.md`, `README.md`

- [ ] **Step 1: Repo-wide gate over the new docs.**

```bash
cd /Users/kalamaha/dev/mediolano-core
grep -rniE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/concepts docs/faq.md
```
Expected: no output. Fix any hit.

- [ ] **Step 2: Cross-link resolve check** — every relative `.md` link in the new docs resolves.

```bash
cd /Users/kalamaha/dev/mediolano-core
for f in docs/concepts/how-it-works.md docs/concepts/ip-protection.md docs/concepts/programmable-licensing.md docs/faq.md; do
  d=$(dirname "$f")
  grep -oE '\(([a-zA-Z0-9_./-]+\.md)(#[a-z-]+)?\)' "$f" | sed -E 's/\((.*)\)/\1/; s/#.*$//' | while read l; do [ -f "$d/$l" ] || echo "BROKEN in $f: $l"; done
done
echo "(no BROKEN lines = all resolve)"
```
Expected: no BROKEN lines.

- [ ] **Step 3: Consistency check** — reread each doc against `05`/`06`/`07` and the axioms; confirm immutability (no admin/owner/upgrade claimed), zero-fee, creator-chooses-license (no pinned default), universality of intelligences, and "owned by no chain" framing. Fix inline.

- [ ] **Step 4: Commit any fixes.**

```bash
git add -A docs/ README.md
git commit -m "docs: final consistency pass on concepts slice" || echo "nothing to fix"
```

---

## Self-Review (completed during plan authoring)

- **Spec coverage:** how-it-works (spec §4.1) → Task 1; ip-protection (§4.2) → Task 2; programmable-licensing (§4.3) → Task 3; faq (§4.4) → Task 4; README surfacing (§3) → Task 5; authoring rules (§6) + default-license stance (§5) enforced by per-task gates + Task 6. Legacy-source corrections (§2) are embedded in Tasks 1–4. No gaps.
- **Placeholder scan:** no TBD/TODO; each task carries concrete content points, sources, links, and exact commands.
- **Consistency:** the gate pattern, link conventions (`../architecture/` from `concepts/`; `architecture/` from `docs/`), and architecture filenames are uniform across tasks and match the spec; license stance ("creator chooses, no pinned default") is identical in Tasks 3, 4, and 6.
