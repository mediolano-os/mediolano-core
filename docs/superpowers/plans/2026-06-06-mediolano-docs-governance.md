# Mediolano Docs — Governance Slice Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Establish Mediolano's public governance documentation — the DAO overview, community & compliance guidelines, and the (draft) constitution and charter — reconciled with the foundation, plus a light `09-stewardship` amendment.

**Architecture:** Five Markdown docs under `docs/governance/` (accessible voice for the overview/guidelines; formal articled voice for the two ratification-pending instruments), an amendment to `docs/architecture/09-stewardship.md`, and README updates. The protocol stays zero-fee; the DAO is funded off-protocol.

**Tech Stack:** Markdown only. Source of truth: `docs/superpowers/specs/2026-06-06-mediolano-docs-governance-design.md`. Legacy sources: `mediolano-app/src/app/docs/`.

**Working branch:** `feat/mediolano-docs-governance` (already created; spec committed there). Do NOT push.

---

## Conventions for every task

- **Docs gate** (governance docs under `docs/governance/`, READMEs):
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' <FILE>
```
Expected: no output. (Present-reality facts allowed: `Snapshot`, `MIP token`, `powered on Starknet`.)
- **Architecture gate** (for the `09` amendment ONLY — stricter, timeless):
```bash
grep -niE 'today|tomorrow|year[ -]?[12]\b|\bv[12]\b|for now|currently|rollout|phase 1|next move|as of|medialane' docs/architecture/09-stewardship.md
```
Expected: no output.
- **Rules:** defer to the axioms; protocol primitives are zero-fee, the DAO is funded off-protocol; do **not** assert a governance-token contract address or any legal status (flag unknowns); the two ⚠ instruments carry a Status box + "Changes from the legacy version" list; all inter-doc links resolve.
- **Link convention:** files in `docs/governance/` link to architecture as `../architecture/NN-*.md`, to siblings as `constitution.md`, to glossary as `../glossary.md`.

---

## Task 1: Amend `09-stewardship.md` (protocol-vs-DAO funding line)

**Files:**
- Modify: `docs/architecture/09-stewardship.md`

- [ ] **Step 1: Add a clarifying subsection.** After the existing "Zero-fee is a hard invariant" section and before "Governance without extraction", insert a subsection that keeps the zero-fee invariant intact and draws the funding line. Use this text:

```markdown
### The protocol is zero-fee; the DAO funds itself off-protocol

Zero-fee is a property of the **primitives**. It is distinct from how the **DAO** sustains its own
stewardship. The DAO may fund itself **off-protocol** — through optional premium services and
app-layer offerings, grants, and donations — and recycle any surplus into public goods. It must
**never** meter, tax, or extract from the primitives to do so. "Governance without extraction"
means no extraction *from the substrate*: the commons stays free to use, while the stewardship
around it can be sustainable.
```

- [ ] **Step 2: Verify.** Run the **architecture** gate on `09-stewardship.md` (must stay timeless) and confirm the zero-fee invariant text is still present.

```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'today|tomorrow|year[ -]?[12]\b|\bv[12]\b|for now|currently|rollout|phase 1|next move|as of|medialane' docs/architecture/09-stewardship.md
grep -c 'zero-fee is a hard invariant\|Zero-fee is a hard invariant\|off-protocol' docs/architecture/09-stewardship.md
```
Expected: gate empty; count ≥ 2.

- [ ] **Step 3: Commit.**

```bash
git add docs/architecture/09-stewardship.md
git commit -m "docs(arch): 09 — clarify protocol-vs-DAO funding (zero-fee primitives; DAO funded off-protocol)"
```

---

## Task 2: `governance/mediolano-dao.md`

**Files:**
- Create: `docs/governance/mediolano-dao.md`
- Read: `mediolano-app/src/app/docs/mediolano-dao/MediolanoDAOContent.tsx`

- [ ] **Step 1: Write the doc** (accessible, layered). Cover:
  - **What the DAO is** — steward of a zero-fee public good; commitments (sustainability of the protocol, open-source for the public/creator economy, censorship-resistant ownership, security & transparency, privacy as a human right).
  - **How it's funded** — off-protocol (optional premium services, grants, donations) recycled into public goods; the protocol primitives stay zero-fee.
  - **Membership & voting** — MIP token membership; open to individuals, organizations, DAOs, and AI agents / autonomous intelligence; Snapshot; 1 token = 1 vote; delegation supported.
  - **Working groups / SubDAOs** — specialized units for development, community, etc.
  - **Stewardship without extraction** — link to `09`.
  - Links: `[Stewardship](../architecture/09-stewardship.md)`, `[Principles](../architecture/01-principles.md)`, `[Axioms](../architecture/00-axioms.md)`.

- [ ] **Step 2: Verify.** Docs gate on the file; confirm link targets exist.
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/governance/mediolano-dao.md
for t in 09-stewardship 01-principles 00-axioms; do [ -f "docs/architecture/$t.md" ] || echo "MISSING $t"; done
```
Expected: gate empty; no MISSING.

- [ ] **Step 3: Commit.**
```bash
git add docs/governance/mediolano-dao.md
git commit -m "docs(governance): Mediolano DAO — mission, funding, membership & voting"
```

---

## Task 3: `governance/community-guidelines.md`

**Files:**
- Create: `docs/governance/community-guidelines.md`
- Read: `mediolano-app/src/app/docs/community-guidelines/CommunityGuidelinesContent.tsx`

- [ ] **Step 1: Write the doc** (accessible). Community norms aligned to the axioms:
  - Permissionless participation; everyone welcome.
  - Respect for all forms of intelligence (human and AI) as equal participants.
  - Integrity, good-faith contribution, transparency.
  - Constructive conduct; no harassment; keep the commons healthy.
  - How to participate (build, contribute, propose) — point to the DAO doc.
  - Links: `[Axioms](../architecture/00-axioms.md)`, `[Mediolano DAO](mediolano-dao.md)`.

- [ ] **Step 2: Verify.** Docs gate; link targets exist (`docs/governance/mediolano-dao.md`, `docs/architecture/00-axioms.md`).

- [ ] **Step 3: Commit.**
```bash
git add docs/governance/community-guidelines.md
git commit -m "docs(governance): community guidelines"
```

---

## Task 4: `governance/compliance-guidelines.md`

**Files:**
- Create: `docs/governance/compliance-guidelines.md`
- Read: `mediolano-app/src/app/docs/compliance-guidelines/ComplianceGuidelinesContent.tsx`

- [ ] **Step 1: Write the doc** (informational). Open with a clear note:

```markdown
> **This is general information, not legal advice.** It describes Mediolano's compliance posture at
> a high level. It makes no claims about the legal or regulatory status of any token, asset, or
> activity in any jurisdiction. Consult qualified counsel for your situation.
```
  Then cover, cautiously and principle-level:
  - **Non-custodial & neutral** — Mediolano is infrastructure; it holds no user assets and authorizes nothing (link `03`).
  - **Authorship & IP** — Berne-aligned, durable records; the protocol records, it does not adjudicate (link `05`).
  - **Securities** — frame cautiously: the documentation asserts **no** securities status for any token or asset; participants are responsible for their own jurisdiction's rules. Flag specifics as items for qualified legal review.
  - **Data & privacy** — data minimization; privacy as a right (link `08`); points to the Privacy Policy (Slice 4, note as forthcoming/deferred).
  - Links: `[Licensing & Authorship](../architecture/05-licensing-and-authorship.md)`, `[Stewardship](../architecture/09-stewardship.md)`.

- [ ] **Step 2: Verify.** Docs gate; confirm the "not legal advice" note present and no asserted legal/securities status.
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/governance/compliance-guidelines.md
grep -ci 'not legal advice' docs/governance/compliance-guidelines.md
```
Expected: gate empty; "not legal advice" count ≥ 1.

- [ ] **Step 3: Commit.**
```bash
git add docs/governance/compliance-guidelines.md
git commit -m "docs(governance): compliance guidelines (informational, not legal advice)"
```

---

## Task 5: `governance/constitution.md` (⚠ DRAFT — pending ratification)

**Files:**
- Create: `docs/governance/constitution.md`
- Read: `mediolano-app/src/app/docs/dao-constitution/ConstitutionContent.tsx`

- [ ] **Step 1: Write the draft.** Open with the Status box, then the changes list, then formal articles. Use this header verbatim:

```markdown
> **Status: DRAFT — pending ratification by the Mediolano DAO. Not yet enacted.**
>
> **Changes from the legacy version**
> - **Treasury realigned:** the DAO is funded **off-protocol** (premium services, grants,
>   donations), not by fees on the protocol. The protocol primitives remain zero-fee.
> - **Zero-fee reconciliation:** language consistent with the architecture's zero-fee invariant.
> - **Chain framing softened:** "powered on Starknet" with the protocol designed to be owned by no
>   chain, rather than Starknet-only.
```
  Then articles (formal voice):
  1. **Name & Purpose** — Mediolano DAO; purpose is to create public goods that empower creators and IP owners; serve creators, developers, collectors, organizations, AI agents, and communities building public goods.
  2. **Principles** — privacy, freedom, transparency, public goods; rooted in the Integrity Web.
  3. **Membership** — via MIP token; open to individuals, legal entities, DAOs, AI agents with verifiable credentials, autonomous intelligence.
  4. **Rights & Responsibilities** — vote proportional to MIP holdings; propose initiatives/amendments; access tooling; maintain sovereignty; uphold integrity; respect all intelligent participation; act in the DAO's interest.
  5. **Governance Process** — proposals via Snapshot; simple majority unless otherwise specified; delegation; minimum holding to submit; timelocked on-chain execution.
  6. **Working Groups & SubDAOs** — specialized units (development, community, etc.).
  7. **Treasury** — funded **off-protocol**; first ensures long-term sustainability of the protocol as a public good; surplus funds open-source tooling and other public goods; recipients commit to transparency and Mediolano principles. (Protocol primitives are zero-fee — no fees taken by the primitives.)
  8. **Amendment** — amendable by DAO process per Article 5.
  - Do **not** assert a token contract address.
  - Links: `[Stewardship](../architecture/09-stewardship.md)`, `[Axioms](../architecture/00-axioms.md)`, `[Governance Charter](governance-charter.md)`.

- [ ] **Step 2: Verify.** Docs gate; confirm Status box + changes list present; no token address asserted.
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/governance/constitution.md
grep -ci 'pending ratification' docs/governance/constitution.md
grep -niE '0x[0-9a-f]{6,}' docs/governance/constitution.md || echo "  (no contract address asserted)"
```
Expected: gate empty; "pending ratification" ≥ 1; no address.

- [ ] **Step 3: Commit.**
```bash
git add docs/governance/constitution.md
git commit -m "docs(governance): DAO constitution (DRAFT, pending ratification)"
```

---

## Task 6: `governance/governance-charter.md` (⚠ DRAFT — pending ratification)

**Files:**
- Create: `docs/governance/governance-charter.md`
- Read: `mediolano-app/src/app/docs/governance-charter/GovernanceCharterContent.tsx`

- [ ] **Step 1: Write the draft.** Same Status box + a changes list (note: funds/compensation sourced off-protocol; zero-fee reconciliation). Then operational rules (formal voice):
  - **Governing principles** — sovereignty (users own their data/IP), transparency (open, verifiable governance), innovation (continuous protocol improvement), inclusivity (anyone can participate).
  - **Proposal lifecycle** — submission (minimum holding may apply), discussion, vote (Snapshot, simple majority unless specified), delegation supported.
  - **Execution** — automatic or timelocked implementation via smart contract.
  - **Use of funds (off-protocol sourced)** — protocol development & maintenance; direct compensation for contributors; public-goods funding. Protocol primitives remain zero-fee.
  - **Relationship to the Constitution** — the charter operationalizes the constitution; the constitution governs on conflict.
  - Links: `[Stewardship](../architecture/09-stewardship.md)`, `[Constitution](constitution.md)`.

- [ ] **Step 2: Verify.** Docs gate; Status box present; link targets exist.
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/governance/governance-charter.md
grep -ci 'pending ratification' docs/governance/governance-charter.md
[ -f docs/governance/constitution.md ] || echo "MISSING constitution.md"
```
Expected: gate empty; "pending ratification" ≥ 1; no MISSING.

- [ ] **Step 3: Commit.**
```bash
git add docs/governance/governance-charter.md
git commit -m "docs(governance): governance charter (DRAFT, pending ratification)"
```

---

## Task 7: Surface Governance in both READMEs

**Files:**
- Modify: `docs/README.md`
- Modify: `README.md`

- [ ] **Step 1: Edit `docs/README.md`.** After the "Concepts" section, add:

```markdown
## Governance

- [Mediolano DAO](governance/mediolano-dao.md) — mission, funding, membership & voting.
- [Community Guidelines](governance/community-guidelines.md) — how the community participates.
- [Compliance Guidelines](governance/compliance-guidelines.md) — informational; not legal advice.
- [Constitution](governance/constitution.md) — *draft, pending ratification.*
- [Governance Charter](governance/governance-charter.md) — *draft, pending ratification.*
```

- [ ] **Step 2: Edit root `README.md`.** After the "Concepts & FAQ" line in the Documentation list, add:

```markdown
- **[Governance](docs/README.md#governance)** — the DAO, guidelines, and governing documents.
```

- [ ] **Step 3: Verify.** Docs gate on both; confirm governance links present.
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/README.md README.md
grep -c 'governance/mediolano-dao.md\|#governance' docs/README.md README.md
```
Expected: gate empty; count ≥ 2.

- [ ] **Step 4: Commit.**
```bash
git add docs/README.md README.md
git commit -m "docs: surface Governance in the docs hub and root README"
```

---

## Task 8: Final consistency pass

**Files:**
- Touch as needed: `docs/governance/*.md`, `docs/architecture/09-stewardship.md`, READMEs

- [ ] **Step 1: Repo-wide docs gate over governance docs.**
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -rniE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/governance
```
Expected: no output.

- [ ] **Step 2: Architecture gate on the amended `09`.**
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'today|tomorrow|year[ -]?[12]\b|\bv[12]\b|for now|currently|rollout|phase 1|next move|as of|medialane' docs/architecture/09-stewardship.md
```
Expected: no output.

- [ ] **Step 3: Cross-link resolve check** for all governance docs.
```bash
cd /Users/kalamaha/dev/mediolano-core
for f in docs/governance/*.md; do
  d=$(dirname "$f")
  grep -oE '\(([a-zA-Z0-9_./-]+\.md)(#[a-z-]+)?\)' "$f" | sed -E 's/\((.*)\)/\1/; s/#.*$//' | while read l; do [ -f "$d/$l" ] || echo "BROKEN in $f: $l"; done
done
echo "(no BROKEN lines = all resolve)"
```
Expected: no BROKEN lines.

- [ ] **Step 4: Consistency check** — reread each doc: zero-fee primitives + off-protocol DAO funding stated consistently; both instruments carry the Status box; no token address or asserted legal status; MIP/Snapshot/1-token-1-vote documented as current. Fix inline.

- [ ] **Step 5: Commit any fixes.**
```bash
git add -A docs/ README.md
git commit -m "docs: final consistency pass on governance slice" || echo "nothing to fix"
```

---

## Self-Review (completed during plan authoring)

- **Spec coverage:** `09` amendment (spec §4) → Task 1; mediolano-dao (§5) → Task 2; community-guidelines (§5) → Task 3; compliance-guidelines (§5) → Task 4; constitution (§5) → Task 5; governance-charter (§5) → Task 6; README surfacing (§3) → Task 7; authoring rules (§6) enforced by per-task gates + Task 8. Treasury reconciliation (§2) appears in Tasks 1, 2, 5, 6. No gaps.
- **Placeholder scan:** no TBD/TODO; each task has concrete content points, the verbatim Status box, sources, links, and exact commands.
- **Consistency:** gates (docs vs architecture) applied to the right files; link conventions uniform; "off-protocol funding," "pending ratification," MIP/Snapshot mechanics phrased identically across tasks and matching the spec.
