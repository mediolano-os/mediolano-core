# Mediolano Core Foundations Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Author the foundational architecture doc set for Mediolano in `mediolano-core` — the public-goods IP-tokenization substrate of the Integrity Web.

**Architecture:** A substrate-tailored, axiom-rooted doc series (`docs/architecture/00-09` + `glossary.md` + `README.md`). Every principle traces to one or more of the 10 Integrity Web Axioms. Docs are foundations-only: chain-agnostic, timeless (no rollout/sequence framing), zero-fee, stands fully alone (no "Medialane" anywhere).

**Tech Stack:** Markdown only. No code, no contracts, no SDK. Source of truth for content: `docs/superpowers/specs/2026-06-06-mediolano-core-foundations-design.md`.

**Working branch:** `feat/mediolano-foundations` (already created; the spec is committed there). Do NOT push.

---

## Conventions for every doc task

- **Voice:** declarative, present-tense, timeless. State what is true *by design*.
- **Forbidden framing (verification-gated):** no temporal words (`today`, `tomorrow`, `year 1/2`, `v1/v2`, `for now`, `currently`, `rollout`, `phase 1`, `next move`, `as of`), and never the string `medialane` (any case). The single allowed temporal usage is naming something explicitly *deferred* (e.g. "the roadmap is a separate effort").
- **Cross-links:** relative links between docs (e.g. `[01 §3](01-principles.md)`).
- **Header:** each doc opens with a one-line purpose and `**Authority:** the [Integrity Web Axioms](00-axioms.md) govern; where this doc conflicts with them, the axioms win.` (the `00` doc itself links to integrityweb.xyz instead).
- **Per-doc verification gate** (run after each draft, before commit):

```bash
cd /Users/kalamaha/dev/mediolano-core
# forbidden temporal framing + cross-entity references (expect: no output)
grep -niE 'today|tomorrow|year[ -]?[12]\b|\bv[12]\b|for now|currently|rollout|phase 1|next move|as of|medialane' docs/architecture/<FILE>.md
```
Expected: **no output** (empty). Any hit must be reworded before commit (unless it is an explicit "deferred" reference, which is allowed and should be re-read to confirm).

---

## Task 1: `00-axioms.md` — The Integrity Web Axioms

**Files:**
- Create: `docs/architecture/00-axioms.md`

- [ ] **Step 1: Write the doc.** Reproduce the 10 axioms verbatim, generic and unmodified. Structure:
  - Title `# 00 — The Integrity Web Axioms`.
  - One-line statement: these are the governing authority (supreme law) of `mediolano-core`; canonical public source: `https://www.integrityweb.xyz/axioms`.
  - Preamble line: *"A Fine Art Declaration of Digital Freedom."*
  - The ten axioms, each as `### AXIOM 0N — <Title>` + the verbatim text:
    1. **Code is Math, Math is Reality** — "All integrity flows from computation. Cryptography is not opinion—it is proof. What is proven is true, and truth is immutable."
    2. **Proof Replaces Trust** — "No authority, no intermediary, no gatekeeper. Trust is not granted—it is mathematically verified. Validity proofs are the foundation of collective confidence."
    3. **Freedom is a Protocol** — "Participation is permissionless. Innovation is open. Censorship is impossible. Freedom is guaranteed by design, not by decree."
    4. **Integrity by Design** — "Every record is tamper-proof. Every action is verifiable. Every identity is self-sovereign. Integrity is not optional—it is embedded in the fabric."
    5. **Public Goods are Sacred** — "Infrastructure belongs to everyone. Proof systems, identity registries, and tokenization protocols are commons. The Integrity Web exists to serve all intelligences equally."
    6. **Privacy is Power** — "Information belongs to its creator. Zero-knowledge ensures autonomy. Privacy is not secrecy—it is sovereignty."
    7. **Decentralization is Resilience** — "No single point of control. No single point of failure. Power is distributed, integrity is preserved."
    8. **Universality of Intelligences** — "Humans, AI agents, and future intelligences share the same rights to participate. The Integrity Web is for all forms of intelligence."
    9. **Creativity is Integrity** — "Knowledge, art, and invention are tokenized as public goods. Ideas are free, yet their integrity is preserved forever."
    10. **The Integrity Web is for Everyone** — "It is censorship-free. It is permissionless. It is universal. It is the trust backbone of digital civilization."
  - Closing note (clearly marked): *Any formal amendment to these axioms is a separate, deliberate future proposal — not made here.*
  - **No commentary, no CROPS mapping, no 11th axiom.**

- [ ] **Step 2: Verify.** Run the verification gate for `00-axioms`. Additionally confirm exactly 10 axioms and the verbatim texts match the list above.

Run: `grep -c '### AXIOM' docs/architecture/00-axioms.md` → Expected: `10`

- [ ] **Step 3: Commit.**

```bash
git add docs/architecture/00-axioms.md
git commit -m "docs(arch): 00 — Integrity Web Axioms (verbatim, supreme law)"
```

---

## Task 2: `01-principles.md` — Principles

**Files:**
- Create: `docs/architecture/01-principles.md`

- [ ] **Step 1: Write the doc.** Structure:
  - Title + purpose ("the load-bearing principles, each derived from the axioms").
  - "What this is" / "Scope": principles constrain every design choice for the Mediolano substrate; when two considerations conflict, the principle wins; principles defer to the axioms.
  - The **11 principles**, each as `### N. <Name>` with: a 2-4 sentence statement, a **Roots:** line citing axiom numbers, and a short **Rules out:** list. Use exactly these principles and roots:
    1. **The contract is the only truth** — chain authorizes; indexers/SDKs/apps cache & present, never authorize. Roots: Ax 01, 02, 04.
    2. **Permissionless & censorship-resistant** — no allowlists/gatekeepers/approval workflows on protocol actions. Roots: Ax 03, 07, 10.
    3. **Immutable primitives** — no admin/owner/upgrade/setters; evolve by redeploy. Roots: Ax 04, 01.
    4. **Zero-fee public-goods substrate** — no fees in the primitives; the infrastructure is a commons. Roots: Ax 05.
    5. **Interoperability over lock-in** — standard token interfaces + metadata; assets usable/understandable outside any single application. Roots: Ax 03, 05, 09.
    6. **Durable, Berne-aligned authorship & licensing** — claims in immutable content-addressed metadata; metadata-first, soft-enforced by default; selective on-chain enforcement only where a service explicitly requires it. Roots: Ax 09, 04.
    7. **Universality of intelligences** — humans, AI agents, organizations, future intelligences are equal first-class participants; no human-only gates. Roots: Ax 08, 05.
    8. **Privacy is sovereignty** — prove without revealing (zk); minimize stored data; never *require* disclosure where a proof suffices. Roots: Ax 06.
    9. **Chain sovereignty** — verifiable trust is a role not a place; portable, re-anchorable identity; users always retain an exit; no single chain is an existential dependency. Roots: Ax 07, 02, 04.
    10. **Self-sovereign identity** — every identity self-sovereign; wallets attach, none required as a gate. Roots: Ax 04, 06.
    11. **Neutral, open, forkable substrate** — anyone can index, fork, or build a competing client; stays useful if any single frontend/indexer/gateway/venue disappears. Roots: Ax 03, 05, 07.
  - A **CROPS** subsection: map Censorship-resistance → principles 2, 9; Open-source → 11; Privacy → 8; Security → 1, 3; state *"longevity over breadth"* as the throughline; note CROPS is the same cypherpunk lineage as the axioms, in another vocabulary (expressed here, deepened in `08`).
  - "How to use this document": a design that violates a principle is a regression unless the principle is amended by consensus (ultimately deferring to the axioms).

- [ ] **Step 2: Verify.** Run the gate for `01-principles`. Confirm all 11 principles have a `Roots:` line citing axiom numbers, and CROPS maps all four letters to principle numbers.

- [ ] **Step 3: Commit.**

```bash
git add docs/architecture/01-principles.md
git commit -m "docs(arch): 01 — Principles (axiom-traced; CROPS expressed)"
```

---

## Task 3: `02-core-model.md` — Core Model

**Files:**
- Create: `docs/architecture/02-core-model.md`

- [ ] **Step 1: Write the doc.** Define the irreducible primitives. For **each** primitive provide three labelled parts — *what it is*, *its identity*, *what it is not*:
  - **Asset** — an IP token on a chain, held by an Account, carrying its License in metadata; identity `(chain, contractAddress, tokenId)`; not a database row, not bound to any application, not the same as its representations on other chains.
  - **Account** — the actor (human, AI agent, organization, collector); the umbrella for everyone who acts; identity via `AccountID` (see `07`); not a wallet (a wallet attaches).
  - **Service** — a protocol module that produces Assets or matches Orders (or both), identified by a stable string ID; the substrate grows by *adding* services (see `06`); not editable-in-place.
  - **License** — the programmable rights in the Asset's metadata (OpenSea-compatible attributes); a *view* on metadata; not a separate entity (see `05`).
  - **Order** — a signed proposal to exchange Assets; settles on the chain it was posted on; not cross-chain by itself.
  - **Event** — an on-chain occurrence indexers consume; a primitive because the indexer's worldview is built from events; not authoritative state itself (the chain is).
  - A short **Roles** section: `creator`, `collector`, `agent`, `organization` are **attributes of Account, never primitives**; roles may gate application *affordances* but never protocol actions (links to principle 2, 7).

- [ ] **Step 2: Verify.** Run the gate for `02-core-model`. Confirm every primitive has the what/identity/what-it-is-not triad and Roles are explicitly not primitives.

- [ ] **Step 3: Commit.**

```bash
git add docs/architecture/02-core-model.md
git commit -m "docs(arch): 02 — Core Model (the irreducible primitives)"
```

---

## Task 4: `03-protocol-and-apps.md` — Protocol & Applications

**Files:**
- Create: `docs/architecture/03-protocol-and-apps.md`

- [ ] **Step 1: Write the doc.** Cover:
  - Mediolano is **neutral substrate**; applications, indexers, SDKs, and agents are consumers.
  - A "what lives where" split: **on-chain = authority** (ownership, balances, mint authority, provenance, order state, service records, events); **off-chain = caches/views** (indexes, search, aggregation, profiles) — rebuildable from chain events.
  - Consumers **present** on-chain reality; they never become the source of truth and never gate protocol actions on off-chain state (link principle 1).
  - The substrate stays fully functional if any single client disappears (link principle 11).
  - No private interfaces: anything one client can do, any client (including AI agents) can do (link principles 7, 11).

- [ ] **Step 2: Verify.** Run the gate for `03-protocol-and-apps`.

- [ ] **Step 3: Commit.**

```bash
git add docs/architecture/03-protocol-and-apps.md
git commit -m "docs(arch): 03 — Protocol & Applications (neutral substrate)"
```

---

## Task 5: `04-interoperability.md` — Interoperability

**Files:**
- Create: `docs/architecture/04-interoperability.md`

- [ ] **Step 1: Write the doc.** Cover:
  - Standard token interfaces (ERC-721 / ERC-1155 and chain-equivalents).
  - The OpenSea-compatible metadata envelope baseline: `name`, `description`, `image`, `animation_url`, `external_url`, `attributes`.
  - Protocol-specific data **extends, never replaces** the baseline; a Mediolano asset must remain understandable outside any Mediolano-specific interface.
  - Interoperability as the **anti-lock-in moat**: assets travel with the creator and remain usable on third-party surfaces (link principle 5).
  - Rule out: behaviors that trap assets (mandatory hooks that fail elsewhere, non-transferable by default) except where a specific service genuinely requires it.

- [ ] **Step 2: Verify.** Run the gate for `04-interoperability`.

- [ ] **Step 3: Commit.**

```bash
git add docs/architecture/04-interoperability.md
git commit -m "docs(arch): 04 — Interoperability (standards over lock-in)"
```

---

## Task 6: `05-licensing-and-authorship.md` — Licensing & Authorship (flagship)

**Files:**
- Create: `docs/architecture/05-licensing-and-authorship.md`

- [ ] **Step 1: Write the doc.** This is the flagship; give it the most depth. Cover:
  - **Berne-Convention alignment:** durable authorship/ownership/license claims that are verifiable independently of any application across Berne jurisdictions (181 countries). Link: `https://en.wikipedia.org/wiki/Berne_Convention`.
  - **Durable records:** authorship/ownership/license claims live in **immutable, content-addressed metadata** (IPFS / Arweave) referenced from the token.
  - **Programmable, metadata-first licensing:** licenses are encoded as OpenSea-compatible metadata attributes (link `04`); a License is a *view* on metadata (link `02`).
  - **Soft enforcement by default:** contracts do not revert on a derivative; enforcement is selective and happens at the application/partner layer. Contracts enforce **only** the specific rules they explicitly implement (escrow, royalty splits, time-locks, access checks).
  - **Why no brittle on-chain legal logic:** contracts are immutable while law changes and varies by jurisdiction; durable *records* belong on-chain / in content-addressed metadata, *enforcement* stays selective and app-layer (link principles 3, 6).
  - Roots throughout: Ax 09 (Creativity is Integrity), Ax 04 (Integrity by Design).

- [ ] **Step 2: Verify.** Run the gate for `05-licensing-and-authorship`. Confirm Berne alignment, content-addressed immutable metadata, soft-by-default + selective enforcement, and the "no brittle on-chain legal logic" rationale are all present.

- [ ] **Step 3: Commit.**

```bash
git add docs/architecture/05-licensing-and-authorship.md
git commit -m "docs(arch): 05 — Licensing & Authorship (Berne-aligned, durable)"
```

---

## Task 7: `06-service-model.md` — Service Model

**Files:**
- Create: `docs/architecture/06-service-model.md`

- [ ] **Step 1: Write the doc.** Cover (principle-level only — no contract enumeration):
  - The central abstraction: the substrate **grows by adding services, not editing them**.
  - A **Service** = a protocol module with a stable string ID, declaring typed **capabilities** (e.g. `mint`, `list`, `buy`, `make_offer`, `cancel`, `transfer`, `license`, `remix`, `claim`, `airdrop`, `escrow`, `subscribe`) — needing behavior outside the set is a signal to *expand the set*, not go free-form.
  - **Marketplace / auction / escrow are services** (neutral primitives) — there is no special commercial "venue" layer and no fee logic in the substrate (link principle 4).
  - Discovery: services are catalogued so wallets, indexers, SDKs, and agents can discover them uniformly (link principles 7, 11).
  - Note: concrete contract families are documented when contracts are tackled — explicitly out of scope here (allowed "deferred" reference).

- [ ] **Step 2: Verify.** Run the gate for `06-service-model`.

- [ ] **Step 3: Commit.**

```bash
git add docs/architecture/06-service-model.md
git commit -m "docs(arch): 06 — Service Model (grow by adding services)"
```

---

## Task 8: `07-identity.md` — Identity

**Files:**
- Create: `docs/architecture/07-identity.md`

- [ ] **Step 1: Write the doc.** Cover:
  - **Self-sovereign identity** (Ax 04: "every identity is self-sovereign").
  - **Account facets:** Wallet (`(chain, address)` — the only thing that can sign; *how* an account acts, not *who*), Account (the logical actor, identified by `AccountID`), Profile (off-chain enrichment, never authoritative).
  - **Two distinct cross-chain mechanisms, never conflated:** **IP-ID** (the same *work* across many chain representations) and **AccountID** (the same *actor* across many wallets, linked by a verifiable signed-attestation graph).
  - **Universality of intelligences** (Ax 08): humans, AI agents, organizations, and future intelligences participate on equal terms; wallets *attach* and none is required as a gate; no human-only flows or anti-agent measures (link principle 7).
  - **Portability** (link principle 9 / `08`): identity must be portable and re-anchorable so it survives any substrate change — anchored on a prover but never solely kept there. Note the concrete re-anchoring *mechanism* is a deferred design task (allowed "deferred" reference).

- [ ] **Step 2: Verify.** Run the gate for `07-identity`. Confirm IP-ID vs AccountID are clearly distinguished and universality-of-intelligences is present.

- [ ] **Step 3: Commit.**

```bash
git add docs/architecture/07-identity.md
git commit -m "docs(arch): 07 — Identity (IP-ID, AccountID, universality of intelligences)"
```

---

## Task 9: `08-chain-sovereignty.md` — Chain Sovereignty

**Files:**
- Create: `docs/architecture/08-chain-sovereignty.md`

- [ ] **Step 1: Write the doc.** Cover (chain-agnostic, timeless — extra care on the verification gate here):
  - **No chain is privileged.** Chain is a first-class dimension everywhere; **Starknet, Ethereum, and Solana are peers**, open-ended for others.
  - **Verifiable trust and settlement are roles behind interfaces**, never hardcoded chain identities — so a role can migrate without rewriting consumers or stranding users.
  - **The protocol is realized by porting Mediolano's own primitives onto each chain** it lives on — never by routing commerce through external venues it does not control. External assets on any chain are freely **indexed** (reading the world is fine).
  - **Portability boundary:** what must survive losing a chain (identity + the work↔actor provenance graph + every user's exit) vs. what may be chain-local (a venue contract, an open order, assets that only lived on that chain).
  - **Users always retain an exit.**
  - **Privacy is a duty of the prover:** the same zk substrate that delivers verifiability also delivers privacy — *prove a claim without revealing the data behind it* — reconciling total verifiability (Ax 01/02/04) with privacy (Ax 06). This is CROPS-Privacy deepened (link principle 8).
  - **Litmus test:** adding a chain touches only an adapter/registry layer; identity and every other chain's path stay untouched.
  - A **CROPS** recap tying C/O/P/S to this doc + the "longevity over breadth" thesis.
  - State that sequencing/implementation status is **out of scope** — a separate roadmap effort (allowed "deferred" reference).

- [ ] **Step 2: Verify.** Run the gate for `08-chain-sovereignty` — this doc is the highest risk for temporal slips; reread every chain reference to confirm peer (not sequenced) framing. Confirm the litmus test and the prove-without-revealing privacy duty are present.

- [ ] **Step 3: Commit.**

```bash
git add docs/architecture/08-chain-sovereignty.md
git commit -m "docs(arch): 08 — Chain Sovereignty (CROPS + multichain, chains as peers)"
```

---

## Task 10: `09-stewardship.md` — Stewardship

**Files:**
- Create: `docs/architecture/09-stewardship.md`

- [ ] **Step 1: Write the doc.** Cover:
  - **Public-goods governance:** a **Mediolano DAO stewards the commons**.
  - **Zero-fee is a hard invariant** — no fees in the immutable primitives, no treasury extraction from the substrate (link principle 4). Explicitly distinct from commercial governance models that allocate fee revenue: the substrate has none to allocate.
  - **The DAO's role:** neutrality-preservation; parameter and opt-in curation decisions that **never become gates** (link principle 2); progressive decentralization — **governance without extraction**.
  - **Public-goods commitment:** the substrate and its proof systems / identity registries are commons (Ax 05); `mediolano-core` itself becomes public when the foundation is finished (allowed "deferred" reference).
  - Rule out: anything that turns stewardship into ownership, gates, or extraction.

- [ ] **Step 2: Verify.** Run the gate for `09-stewardship`. Confirm zero-fee-as-hard-invariant and governance-without-extraction are present.

- [ ] **Step 3: Commit.**

```bash
git add docs/architecture/09-stewardship.md
git commit -m "docs(arch): 09 — Stewardship (DAO governance of a zero-fee commons)"
```

---

## Task 11: `glossary.md` — Canonical terms

**Files:**
- Create: `docs/glossary.md`

- [ ] **Step 1: Write the doc.** Alphabetical-ish grouped glossary covering: the six primitives (Asset, Account, Service, License, Order, Event); identity terms (Wallet, AccountID, IP-ID, Profile); service/capability vocabulary (Capability, Service registry, soft enforcement); CROPS; chain-sovereignty terms (prover role, portability boundary, exit, litmus test); Berne Convention; Integrity Web; Mediolano. Each entry: one to three sentences, linking to the governing doc. Header note: "where this conflicts with `architecture/`, the architecture governs."

- [ ] **Step 2: Verify.** Run the gate for `glossary` (path `docs/glossary.md`). Confirm each term links to its governing doc.

Run: `cd /Users/kalamaha/dev/mediolano-core && grep -niE 'today|tomorrow|year[ -]?[12]\b|\bv[12]\b|for now|currently|rollout|phase 1|next move|as of|medialane' docs/glossary.md` → Expected: no output.

- [ ] **Step 3: Commit.**

```bash
git add docs/glossary.md
git commit -m "docs: glossary of canonical Mediolano terms"
```

---

## Task 12: `README.md` — Docs index

**Files:**
- Create: `docs/README.md`

- [ ] **Step 1: Write the doc.** An index for `mediolano-core/docs`: a one-line description of Mediolano, the statement that the **axioms (`00`) are the governing authority**, the reading order (`00`→`09`), a one-line description per architecture doc + glossary, and a pointer to `superpowers/specs` and `superpowers/plans` for design history.

- [ ] **Step 2: Verify.** Run the gate for `README` (path `docs/README.md`). Confirm every `00-09` doc + glossary is listed in order.

- [ ] **Step 3: Commit.**

```bash
git add docs/README.md
git commit -m "docs: README index + reading order for mediolano-core"
```

---

## Task 13: Final consistency pass

**Files:**
- Touch as needed: any of `docs/architecture/*.md`, `docs/glossary.md`, `docs/README.md`

- [ ] **Step 1: Repo-wide forbidden-framing sweep.**

Run:
```bash
cd /Users/kalamaha/dev/mediolano-core
grep -rniE 'today|tomorrow|year[ -]?[12]\b|\bv[12]\b|for now|currently|rollout|phase 1|next move|as of|medialane' docs/architecture docs/glossary.md docs/README.md
```
Expected: no output except lines that are explicit *deferred*-scope references (reread each hit to confirm it is a deferred reference, not a slip). Fix any real slip.

- [ ] **Step 2: Axiom-traceability check.** Confirm `01-principles.md` cites axiom numbers on all 11 principles, and that every doc's `Authority:` line points to `00-axioms.md`.

Run: `grep -L 'axioms.md' docs/architecture/0[1-9]*.md` → Expected: no output (every 01-09 doc references the axioms).

- [ ] **Step 3: Cross-link check.** Verify inter-doc links resolve (filenames exist).

Run:
```bash
cd /Users/kalamaha/dev/mediolano-core/docs && ls architecture/00-axioms.md architecture/01-principles.md architecture/02-core-model.md architecture/03-protocol-and-apps.md architecture/04-interoperability.md architecture/05-licensing-and-authorship.md architecture/06-service-model.md architecture/07-identity.md architecture/08-chain-sovereignty.md architecture/09-stewardship.md glossary.md README.md
```
Expected: all 12 files listed, no "No such file".

- [ ] **Step 4: Commit any fixes.**

```bash
git add -A docs/
git commit -m "docs: final consistency pass (framing, traceability, cross-links)" || echo "nothing to fix"
```

---

## Self-Review (completed during plan authoring)

- **Spec coverage:** every spec §5 doc maps to a task (00→T1, 01→T2, 02→T3, 03→T4, 04→T5, 05→T6, 06→T7, 07→T8, 08→T9, 09→T10, glossary→T11, README→T12); §2 authoring philosophy enforced via the per-doc gate + T13; §7 out-of-scope honored (no contract/SDK work, no roadmap doc, no axiom amendment, no publish, no Medialane). No gaps.
- **Placeholder scan:** no "TBD/TODO/implement later"; each task carries the actual required content points and exact verification commands.
- **Type/term consistency:** primitive names (Asset/Account/Service/License/Order/Event), identity terms (IP-ID/AccountID/Wallet/Profile), and CROPS letter→principle mappings are identical across tasks and match the spec.
