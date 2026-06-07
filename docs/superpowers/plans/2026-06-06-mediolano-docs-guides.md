# Mediolano Docs — Guides Slice Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Write the protocol-level "Build on Mediolano" developer guide and surface it (plus an app pointer) in the READMEs.

**Architecture:** One Markdown doc, `docs/guides/build-on-mediolano.md`, principle-level and accessible, with the app usage/setup guides kept app-side (core links to them). README updates only otherwise.

**Tech Stack:** Markdown only. Source of truth: `docs/superpowers/specs/2026-06-06-mediolano-docs-guides-design.md`. Legacy sources (review only): `mediolano-app/src/app/docs/{developers,permissionless-setup}/`.

**Working branch:** `feat/mediolano-docs-guides` (already created; spec committed there). Do NOT push.

---

## Conventions

- **Docs gate** (after each draft, before commit):
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' <FILE>
```
Expected: no output.
- **No hardcoded contract addresses; no asserted `@mediolano/sdk`/REST API/Subgraphs; org is `mediolano-os`.**
- **Link convention:** files in `docs/guides/` link to architecture as `../architecture/NN-*.md`, to the hub as `../README.md`, to glossary as `../glossary.md`.

---

## Task 1: `guides/build-on-mediolano.md`

**Files:**
- Create: `docs/guides/build-on-mediolano.md`
- Read (review only, correct — do not copy): `mediolano-app/src/app/docs/developers/DevelopersContent.tsx`, `mediolano-app/src/app/docs/permissionless-setup/PermissionlessSetupContent.tsx`

- [ ] **Step 1: Write the doc** (accessible, layered, principle-level). Sections:
  1. **Build without asking** — Mediolano is a public, permissionless, zero-fee, immutable substrate; anyone can build on it with no gatekeeper and no permission.
  2. **What you build on** — the immutable contracts (`mediolano-os/mediolano-contracts`); on-chain state is the source of truth; standard token interfaces and metadata make assets readable everywhere.
  3. **Three ways to build** —
     - **Read & index** on-chain state — build clients, explorers, indexers, analytics.
     - **Interact** with existing service contracts — use the protocol's capabilities directly.
     - **Deploy** your own service contracts that compose with the protocol — the substrate grows by *adding* services. → [Service Model](../architecture/06-service-model.md).
     All permissionless, non-custodial, zero-fee.
  4. **AI agents are first-class** — agents build and act on the same terms as humans; state and metadata are machine-readable. → [Identity](../architecture/07-identity.md).
  5. **Resources** — the [`mediolano-os` GitHub org](https://github.com/mediolano-os), [`mediolano-os/mediolano-contracts`](https://github.com/mediolano-os/mediolano-contracts), the [architecture](../README.md), the [glossary](../glossary.md). Note tooling/SDKs are evolving and are not asserted here.
  6. **Using the reference app** — to *use* Mediolano (rather than build on it), see the IP Creator at <https://ip.mediolano.app>; its usage and local-setup guides live with the app, not in the protocol core.
  - Header links: [Protocol & Applications](../architecture/03-protocol-and-apps.md), [Service Model](../architecture/06-service-model.md), [Identity](../architecture/07-identity.md).

- [ ] **Step 2: Verify.** Docs gate; confirm no addresses, no asserted SDK/API, org is correct, link targets exist.
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/guides/build-on-mediolano.md
grep -niE '0x[0-9a-f]{6,}|@mediolano/sdk|openapi|subgraph|mediolano-app/mediolano' docs/guides/build-on-mediolano.md || echo "  (no addresses / asserted SDK / old-org refs)"
for t in 03-protocol-and-apps 06-service-model 07-identity; do [ -f "docs/architecture/$t.md" ] || echo "MISSING $t"; done
[ -f docs/README.md ] && [ -f docs/glossary.md ] || echo "MISSING hub/glossary"
```
Expected: gate empty; no addresses/SDK/old-org; no MISSING.

- [ ] **Step 3: Commit.**
```bash
git add docs/guides/build-on-mediolano.md
git commit -m "docs(guides): build on Mediolano — protocol-level developer guide"
```

---

## Task 2: Surface in both READMEs

**Files:**
- Modify: `docs/README.md`
- Modify: `README.md`

- [ ] **Step 1: Edit `docs/README.md`.** After the "Policy" section (and before "Supporting reference"), add:

```markdown
## Build

- [Build on Mediolano](guides/build-on-mediolano.md) — how to build on the protocol.

To *use* Mediolano, see the IP Creator at <https://ip.mediolano.app> (its usage and setup guides
live with the app).
```

- [ ] **Step 2: Edit root `README.md`.** After the "Policy" line in the Documentation list, add:

```markdown
- **[Build on Mediolano](docs/guides/build-on-mediolano.md)** — for developers building on the protocol.
```

- [ ] **Step 3: Verify.** Docs gate on both; confirm the build link present.
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -niE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/README.md README.md
grep -c 'guides/build-on-mediolano.md' docs/README.md README.md
```
Expected: gate empty; count ≥ 2.

- [ ] **Step 4: Commit.**
```bash
git add docs/README.md README.md
git commit -m "docs: surface Build guide in the docs hub and root README"
```

---

## Task 3: Final consistency pass

**Files:**
- Touch as needed: `docs/guides/build-on-mediolano.md`, READMEs

- [ ] **Step 1: Gate + cross-link resolve.**
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -rniE 'medialane|roadmap|coming soon|will launch|next quarter|by 202[0-9]|q[1-4] 202[0-9]' docs/guides
d=docs/guides
grep -oE '\(([a-zA-Z0-9_./-]+\.md)(#[a-z-]+)?\)' docs/guides/build-on-mediolano.md | sed -E 's/\((.*)\)/\1/; s/#.*$//' | while read l; do [ -f "$d/$l" ] || echo "BROKEN: $l"; done
echo "(no output above = clean + links resolve)"
```
Expected: no output.

- [ ] **Step 2: Consistency check** — reread: permissionless/zero-fee/non-custodial stated; no addresses; no asserted SDK; org `mediolano-os`; AI agents first-class; app pointer present. Fix inline.

- [ ] **Step 3: Commit any fixes.**
```bash
git add -A docs/ README.md
git commit -m "docs: final consistency pass on guides slice" || echo "nothing to fix"
```

---

## Self-Review (completed during plan authoring)

- **Spec coverage:** build-on-mediolano (spec §5) → Task 1; README surfacing + app pointer (§4) → Task 2; corrections (§3) embedded in Task 1 and checked in Tasks 1 & 3; authoring rules (§6) enforced by gates. App guides stay app-side (§2, §7) — nothing to do in core. No gaps.
- **Placeholder scan:** no TBD/TODO; Task 1 carries concrete sections, links, and exact commands.
- **Consistency:** gate pattern, link conventions, org name (`mediolano-os`), and "no addresses / no asserted SDK" rule are uniform and match the spec.
