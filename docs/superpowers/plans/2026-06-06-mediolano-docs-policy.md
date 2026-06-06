# Mediolano Docs — Policy / Legal Slice Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Write the Terms of Use and Privacy Policy (drafts pending legal review) and the Security doc, corrected against the foundation.

**Architecture:** Three Markdown docs under `docs/policy/` — `terms-of-use` and `privacy-policy` as legal drafts (Status box + flagged changes), `security` as a non-custodial rewrite — plus README updates.

**Tech Stack:** Markdown only. Source of truth: `docs/superpowers/specs/2026-06-06-mediolano-docs-policy-design.md`. Legacy sources: `mediolano-app/src/app/docs/`.

**Working branch:** `feat/mediolano-docs-policy` (already created; spec committed there). Do NOT push.

---

## Conventions for every task

- **Docs gate** (after each draft, before commit):
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' <FILE>
```
Expected: no output. (Present-reality facts allowed: `powered on Starknet`.)
- **Rules:** defer to the axioms; assert no legal status, jurisdiction, legal entity, or token address; flag unknowns. The two ⚠ drafts carry the Status box + "Changes from the legacy version" list. All inter-doc links resolve.
- **Link convention:** files in `docs/policy/` link to architecture as `../architecture/NN-*.md`, to governance as `../governance/*.md`, to siblings as `security.md`.
- **Berne:** use "180+ Berne member states" and frame as *evidence aligned with Berne* (never "tokenization confers recognition").

---

## Task 1: `policy/terms-of-use.md` (⚠ DRAFT — pending legal review)

**Files:**
- Create: `docs/policy/terms-of-use.md`
- Read: `mediolano-app/src/app/docs/terms-of-use/TermsOfUseContent.tsx`

- [ ] **Step 1: Write the draft.** Open with this box verbatim:

```markdown
> **Status: DRAFT — pending legal review. Not yet in force.**
> This is general information, not legal advice.
>
> **Changes from the legacy version**
> - **Berne overclaim corrected:** Mediolano produces verifiable authorship *evidence* aligned
>   with the Berne Convention; recognition flows from authorship of the work, not from tokenization.
> - **Count standardized:** "180+ Berne member states" (exact figure pending legal review).
> - **Zero-fee & non-custodial made explicit;** chain framing aligned to "owned by no chain."
```
  Then sections:
  - **1. Acceptance of terms** — using the protocol or apps constitutes agreement; terms are amendable through Mediolano DAO governance.
  - **2. What Mediolano is** — permissionless, open-source protocol; non-custodial; primitives are zero-fee; produces Berne-aligned authorship evidence.
  - **3. Eligibility & responsible use** — lawful use only; you are responsible for the works you tokenize and for holding the rights to them.
  - **4. Your assets & keys** — you control your own assets and keys; Mediolano holds nothing and cannot move or freeze your assets.
  - **5. Intellectual property** — authorship/ownership records are *evidence*, not adjudication; **jurisdictional enforcement remains the creator's responsibility**; Berne protection term is typically 50–70 years depending on jurisdiction.
  - **6. No fees at the protocol layer** — the primitives take no fee; applications may have their own terms.
  - **7. Disclaimers & risk** — provided "as is"; software and smart-contract risk; see [Security](security.md).
  - **8. Governance & amendment** — these terms evolve through DAO governance.
  - Links: `[Licensing & Authorship](../architecture/05-licensing-and-authorship.md)`, `[Mediolano DAO](../governance/mediolano-dao.md)`, `[Security](security.md)`.

- [ ] **Step 2: Verify.** Docs gate; confirm Status box, no recognition overclaim, link targets exist.
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/policy/terms-of-use.md
grep -ci 'pending legal review' docs/policy/terms-of-use.md
grep -niE 'recognized under the berne|tokenized ip is recognized' docs/policy/terms-of-use.md || echo "  (no recognition overclaim)"
for t in ../architecture/05-licensing-and-authorship.md ../governance/mediolano-dao.md security.md; do [ -f "docs/policy/$t" ] || ( cd docs/policy && [ -f "$t" ] ) || echo "MISSING $t"; done
```
Expected: gate empty; "pending legal review" ≥ 1; no overclaim; no MISSING.

- [ ] **Step 3: Commit.**
```bash
git add docs/policy/terms-of-use.md
git commit -m "docs(policy): terms of use (DRAFT, pending legal review)"
```

---

## Task 2: `policy/privacy-policy.md` (⚠ DRAFT — pending legal review)

**Files:**
- Create: `docs/policy/privacy-policy.md`
- Read: `mediolano-app/src/app/docs/privacy-policy/PrivacyPolicyContent.tsx`

- [ ] **Step 1: Write the draft.** Open with this box verbatim:

```markdown
> **Status: DRAFT — pending legal review. Not yet in force.**
> This is general information, not legal advice.
>
> **Changes from the legacy version**
> - **Aligned to the Privacy axiom:** data minimization and prove-without-revealing made central.
> - **Cookie handling folded in;** removed the dangling separate "Cookie Policy" reference.
> - **On-chain publicity clarified;** chain framing aligned to "owned by no chain."
```
  Then sections:
  - **1. Our stance** — privacy is a right (Axiom 06); the protocol favors data minimization and proving claims without revealing the data behind them.
  - **2. What we collect** — minimal; **no default cookies, trackers, or behavioral analytics.**
  - **3. On-chain data is public** — transactions, authorship, and ownership recorded on a blockchain are public by nature and not private; understand this before tokenizing.
  - **4. Cookies** — the dapp avoids cookies and similar technologies (folded in; no separate policy).
  - **5. Your control** — non-custodial; you hold your keys and your data.
  - **6. Contact** — `mediolanoapp@gmail.com` (provisional, pending legal review).
  - Links: `[Chain Sovereignty](../architecture/08-chain-sovereignty.md)`, `[Stewardship](../architecture/09-stewardship.md)`.

- [ ] **Step 2: Verify.** Docs gate; Status box; minimal-data present; no dangling Cookie Policy doc reference.
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/policy/privacy-policy.md
grep -ci 'pending legal review' docs/policy/privacy-policy.md
grep -niE 'cookie policy' docs/policy/privacy-policy.md || echo "  (no separate Cookie Policy reference)"
```
Expected: gate empty; "pending legal review" ≥ 1; no "Cookie Policy" doc reference.

- [ ] **Step 3: Commit.**
```bash
git add docs/policy/privacy-policy.md
git commit -m "docs(policy): privacy policy (DRAFT, pending legal review)"
```

---

## Task 3: `policy/security.md` (rewrite)

**Files:**
- Create: `docs/policy/security.md`
- Read: `mediolano-app/src/app/docs/security/SecurityContent.tsx`

- [ ] **Step 1: Write the doc.** Sections:
  - Opening note: *general information, not financial advice.*
  - **1. Security posture** — immutable primitives (no admin/owner/upgrade); audits; a verifiable end-to-end stack; CROPS-Security.
  - **2. Non-custodial by design** — Mediolano holds nothing and can freeze nothing; you control your own assets and keys. Risk is to **your own self-custodied assets**, not to funds held by Mediolano.
  - **3. Inherent risks** — smart contracts carry risk; despite audits and testing, bugs in the protocol or the underlying network (Starknet/Ethereum) could put your assets at risk. Use caution.
  - **4. Good practices** — guard your keys; verify contracts and metadata; understand a transaction before signing.
  - **5. Responsible disclosure** — security reports are welcome; a dedicated disclosure channel is being established (provisional — flag).
  - Links: `[Principles](../architecture/01-principles.md)`, `[Chain Sovereignty](../architecture/08-chain-sovereignty.md)`.

- [ ] **Step 2: Verify.** Docs gate; confirm non-custodial framing (no "funds held by Mediolano") and link targets.
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/policy/security.md
grep -ci 'non-custodial\|self-custodied\|holds nothing' docs/policy/security.md
for t in ../architecture/01-principles.md ../architecture/08-chain-sovereignty.md; do ( cd docs/policy && [ -f "$t" ] ) || echo "MISSING $t"; done
```
Expected: gate empty; non-custodial count ≥ 1; no MISSING.

- [ ] **Step 3: Commit.**
```bash
git add docs/policy/security.md
git commit -m "docs(policy): security — non-custodial posture, risks, disclosure"
```

---

## Task 4: Surface Policy in both READMEs

**Files:**
- Modify: `docs/README.md`
- Modify: `README.md`

- [ ] **Step 1: Edit `docs/README.md`.** After the "Governance" section, add:

```markdown
## Policy

- [Terms of Use](policy/terms-of-use.md) — *draft, pending legal review.*
- [Privacy Policy](policy/privacy-policy.md) — *draft, pending legal review.*
- [Security](policy/security.md) — security posture, risks, and disclosure.
```

- [ ] **Step 2: Edit root `README.md`.** After the "Governance" line in the Documentation list, add:

```markdown
- **[Policy](docs/README.md#policy)** — terms, privacy, and security.
```

- [ ] **Step 3: Verify.** Docs gate on both; confirm policy links present.
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/README.md README.md
grep -c 'policy/terms-of-use.md\|#policy' docs/README.md README.md
```
Expected: gate empty; count ≥ 2.

- [ ] **Step 4: Commit.**
```bash
git add docs/README.md README.md
git commit -m "docs: surface Policy in the docs hub and root README"
```

---

## Task 5: Final consistency pass

**Files:**
- Touch as needed: `docs/policy/*.md`, READMEs

- [ ] **Step 1: Repo-wide docs gate over policy.**
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -rniE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/policy
```
Expected: no output.

- [ ] **Step 2: Cross-link resolve for policy docs.**
```bash
cd /Users/kalamaha/dev/mediolano-core
for f in docs/policy/*.md; do
  d=$(dirname "$f")
  grep -oE '\(([a-zA-Z0-9_./-]+\.md)(#[a-z-]+)?\)' "$f" | sed -E 's/\((.*)\)/\1/; s/#.*$//' | while read l; do [ -f "$d/$l" ] || echo "BROKEN in $f: $l"; done
done
echo "(no BROKEN lines = all resolve)"
```
Expected: no BROKEN lines.

- [ ] **Step 3: Consistency check** — reread each doc: Berne framed as evidence (no recognition overclaim, "180+ member states"); non-custodial + zero-fee stated; data minimization in privacy; both ⚠ drafts carry the Status box; no asserted legal status/jurisdiction/token address. Fix inline.

- [ ] **Step 4: Commit any fixes.**
```bash
git add -A docs/ README.md
git commit -m "docs: final consistency pass on policy slice" || echo "nothing to fix"
```

---

## Self-Review (completed during plan authoring)

- **Spec coverage:** terms-of-use (spec §5) → Task 1; privacy-policy (§5) → Task 2; security (§5) → Task 3; README surfacing (§4) → Task 4; corrections (§3) embedded in Tasks 1–3 and re-checked in Task 5; authoring rules (§6) enforced by per-task gates. No gaps.
- **Placeholder scan:** no TBD/TODO; each task carries the verbatim Status boxes, concrete sections, sources, links, and exact commands.
- **Consistency:** gate pattern, link conventions (`../architecture/`, `../governance/`, sibling), Berne phrasing ("180+ member states", evidence framing), and non-custodial language are uniform across tasks and match the spec.
