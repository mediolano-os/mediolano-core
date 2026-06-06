# Mediolano Core Foundations — Design Spec

**Date:** 2026-06-06
**Status:** Draft for review.
**Repo:** `mediolano-core` (documentation only — no contract, SDK, indexer, or app changes this pass).
**Scope:** Establish the foundational architecture doc set for **Mediolano** — the public-goods
intellectual-property tokenization substrate of the Integrity Web.

---

## 1. Goal

Bring the **Integrity Web Axioms** into `mediolano-core` as its constitution, and build a
foundational architecture doc set that expresses Mediolano on its own terms: a permissionless,
zero-fee, immutable, **multichain**, **CROPS-aligned** public good for tokenizing, protecting,
licensing, and composing intellectual property — **Berne-Convention-aligned** and open to **all
intelligences, from human to future AI**.

This pass produces the *foundation*. It does not touch contracts, and it does not schedule work.

---

## 2. Authoring philosophy (how every doc in this set is written)

These rules are load-bearing for the writing itself, not just the content:

- **Foundations, not timelines.** The docs state what is true *by design*. There is **no
  "today/tomorrow," no "v1/year-1," no phased rollout, no deployment status** anywhere in the
  foundation. Sequencing and implementation status belong to a later, separate roadmap
  brainstorm — deliberately out of scope here.
- **Chain-agnostic by construction.** No chain is privileged or "primary." Chain is a
  first-class dimension; the prover/settlement function is a **role behind an interface**.
  Starknet, Ethereum, and Solana are **peers**. Multichain is a *property of the foundation*,
  not a feature added later.
- **Axiom-rooted.** Every principle traces to one or more of the 10 Integrity Web Axioms. The
  axioms govern; where any doc conflicts with them, the axioms win.
- **Stands fully alone.** Mediolano is described entirely on its own terms. No reference to any
  particular commercial layer by name; where a consumer must be named, use generic terms
  ("applications," "marketplaces," "commercial layers," "indexers," "agents").
- **Substrate, not app.** Mediolano is neutral infrastructure. **No fee model, no commercial
  venue layer.** The substrate is zero-fee and neutral; applications build their own models
  around it.

---

## 3. Decisions locked during brainstorming

- **Structure:** purpose-built, substrate-tailored doc set (not a clone of any commercial-app
  doc set). Commercial artifacts (a fee/treasury model, a separate "venue" doc) are excluded.
- **Axioms:** the 10 Integrity Web Axioms reproduced **verbatim and unmodified**, kept generic
  and unrestrictive, as supreme law. **No CROPS text injected into the axioms doc**; no 11th
  axiom; no renumber. CROPS is *expressed* in `01-principles` and *deepened* in
  `08-chain-sovereignty`.
- **Privacy** stays as **Axiom 06 ("Privacy is Power")** — reinforced through the principles and
  the zk "prove-without-revealing" duty, not added as a new axiom.
- **Roadmap deferred.** No `10-trajectory` doc this pass — it gets its own brainstorm once the
  foundation is solved.
- **DAO governance is part of the foundation** — captured in `09-stewardship` as *public-goods*
  governance (a DAO that stewards a zero-fee commons; governance without extraction).
- **Multichain direction** (recorded in `08`, without any timeline): the protocol is realized by
  **porting Mediolano's own primitives onto each chain** it lives on — Starknet, Ethereum,
  Solana as peers, open-ended for others — never by renting external venues.
- **Protocol-facing docs (05/06/07) are written at the architecture/principle level.** No
  reading or auditing of `mediolano-contracts` this pass.
- **Stands alone:** no mention of Medialane (an unrelated entity).

---

## 4. Deliverable & file layout

All within `mediolano-core`:

```
docs/
  architecture/
    00-axioms.md                    # The 10 Integrity Web Axioms, verbatim — supreme law
    01-principles.md                # Load-bearing principles, each traced to axiom(s); CROPS expressed
    02-core-model.md                # The irreducible primitives
    03-protocol-and-apps.md         # Neutral substrate; apps consume, never authorize
    04-interoperability.md          # Standard token interfaces + metadata envelopes
    05-licensing-and-authorship.md  # Berne-aligned, programmable, soft-enforced, durable
    06-service-model.md             # Service taxonomy; substrate grows by adding services
    07-identity.md                  # IP-ID, AccountID, cross-chain, universality of intelligences
    08-chain-sovereignty.md         # CROPS + multichain invariants; privacy via zk
    09-stewardship.md               # DAO governance as zero-fee public-goods stewardship
  glossary.md                       # Canonical terms
  README.md                         # Index + reading order
```

(`10-trajectory.md` intentionally absent — deferred.)

---

## 5. Document specifications

### `00-axioms.md` — The Integrity Web Axioms
The **10 axioms reproduced verbatim** (preamble: *"A Fine Art Declaration of Digital Freedom"*),
kept generic and unrestrictive. A single short header stating they are `mediolano-core`'s
governing authority, plus the canonical public source (`integrityweb.xyz/axioms`). **No
commentary, no CROPS mapping, no added axiom.** One clearly-marked forward note: *any formal
amendment to the axioms is a separate, deliberate future proposal — not made here.*

The ten (titles): 01 Code is Math, Math is Reality · 02 Proof Replaces Trust · 03 Freedom is a
Protocol · 04 Integrity by Design · 05 Public Goods are Sacred · 06 Privacy is Power · 07
Decentralization is Resilience · 08 Universality of Intelligences · 09 Creativity is Integrity ·
10 The Integrity Web is for Everyone.

### `01-principles.md` — Principles
The load-bearing principles, each traced to its axiom(s). This is the heart of the foundation.

| # | Principle | Roots |
|---|-----------|-------|
| 1 | **The contract is the only truth** — the chain authorizes; indexers/SDKs/apps cache and present, never authorize | Ax 01, 02, 04 |
| 2 | **Permissionless & censorship-resistant** — no allowlists, no gatekeepers, no approval workflows on protocol actions | Ax 03, 07, 10 |
| 3 | **Immutable primitives** — no admin/owner/upgrade/setters; evolve by redeploy, not mutation | Ax 04, 01 |
| 4 | **Zero-fee public-goods substrate** — no fees in the primitives; the infrastructure is a commons | Ax 05 |
| 5 | **Interoperability over lock-in** — standard token interfaces + metadata; assets remain usable and understandable outside any single application | Ax 03, 05, 09 |
| 6 | **Durable, Berne-aligned authorship & licensing** — authorship/ownership/license claims in immutable, content-addressed metadata; metadata-first, soft-enforced by default; selective on-chain enforcement only where a service explicitly requires it | Ax 09, 04 |
| 7 | **Universality of intelligences** — humans, AI agents, organizations, and future intelligences are equal, first-class participants; no human-only gates | Ax 08, 05 |
| 8 | **Privacy is sovereignty** — prove without revealing (zk); minimize stored data; never *require* disclosure where a proof suffices | Ax 06 |
| 9 | **Chain sovereignty** — verifiable trust is a role, not a place; identity is portable and re-anchorable; users always retain an exit; no single chain is an existential dependency | Ax 07, 02, 04 |
| 10 | **Self-sovereign identity** — every identity is self-sovereign; wallets *attach*, none required as a gate | Ax 04, 06 |
| 11 | **Neutral, open, forkable substrate** — anyone can index, fork, or build a competing client; the substrate stays useful if any single frontend/indexer/gateway/venue disappears | Ax 03, 05, 07 |

**CROPS expressed:** Censorship-resistance (2, 9) · Open-source (11) · Privacy (8) · Security
(1, 3) — with *"longevity over breadth"* as the throughline. Closes with a governance clause: a
design that violates a principle is a regression unless the principle is amended by consensus
(deferring ultimately to the axioms).

### `02-core-model.md` — Core Model
The irreducible primitives of the substrate, each defined by *what it is*, *its identity*, and
*what it is not*: **Asset** (an IP token on a chain, carrying its License in metadata),
**Account** (the actor — human, AI agent, organization, collector), **Service** (a protocol
module identified by a stable ID), **License** (a view on the Asset's metadata), **Order** (a
signed proposal to exchange Assets), **Event** (the on-chain occurrence indexers consume). Roles
(creator/collector/agent/organization) are **attributes of Account, never primitives**.

### `03-protocol-and-apps.md` — Protocol & Applications
Mediolano is **neutral substrate**. What lives on-chain (authority) vs. what lives off-chain
(caches, views). Applications, indexers, SDKs, and agents are consumers that present on-chain
reality; they never become the source of truth. The substrate remains fully functional if any
single client disappears. No private interfaces; anything one client can do, any client can do.

### `04-interoperability.md` — Interoperability
Standard token interfaces (ERC-721 / ERC-1155 and chain-equivalents) and an OpenSea-compatible
metadata envelope (`name`, `description`, `image`, `animation_url`, `external_url`,
`attributes`). Protocol-specific data **extends, never replaces** the baseline. A Mediolano
asset is understandable outside any Mediolano-specific interface. Interoperability is the
anti-lock-in moat.

### `05-licensing-and-authorship.md` — Licensing & Authorship *(flagship)*
**Berne-Convention-aligned durable authorship.** Authorship, ownership, and license claims live
in **immutable, content-addressed metadata** (IPFS / Arweave) referenced from the token, so they
are verifiable independently of any application across all Berne jurisdictions. Licensing is
**programmable, metadata-first, soft-enforced by default**; contracts enforce only the specific
rules they explicitly implement (escrow, royalty splits, time-locks, access checks). Rationale
for **no brittle on-chain legal logic**: contracts are immutable while law changes and varies by
jurisdiction — so durable *records* live on-chain/in content-addressed metadata, while
*enforcement* is selective and app-layer.

### `06-service-model.md` — Service Model
The substrate **grows by adding services, not editing them**. A Service is a protocol module with
a stable ID declaring typed **capabilities** (mint, list, buy, offer, license, remix, claim,
airdrop, escrow, subscribe, …). Marketplace / auction / escrow are **services (neutral
primitives)** — there is no special commercial "venue" layer. Written at the principle level;
the concrete contract families are documented when contracts are tackled (later, out of scope).

### `07-identity.md` — Identity
**Self-sovereign identity** (Ax 04). Two distinct cross-chain mechanisms, never conflated:
**IP-ID** (the same *work* across many chain representations) and **AccountID** (the same *actor*
across many wallets, linked by signed attestations). **Universality of intelligences** (Ax 08):
humans, AI agents, organizations, and future intelligences participate on equal terms; wallets
*attach* to an Account and none is required as a gate; no human-only flows or anti-agent
measures. Identity is **portable and re-anchorable** so it survives any substrate change.

### `08-chain-sovereignty.md` — Chain Sovereignty
The CROPS + multichain foundation, **chain-agnostic and timeless**. No chain is privileged.
Verifiable trust and settlement are **roles filled behind interfaces**, never hardcoded chain
identities. The protocol is realized by **porting Mediolano's own primitives onto each chain**
it lives on — **Starknet, Ethereum, Solana as peers**, open-ended for others — never by routing
commerce through external venues it does not control (external assets are freely *indexed*).
**Identity is portable; users always retain an exit.** **Privacy is a duty of the prover**: the
same zk substrate that delivers verifiability also delivers privacy — *prove a claim without
revealing the data behind it* — reconciling total verifiability (Ax 01/02/04) with privacy
(Ax 06). **Litmus test:** adding a chain touches only an adapter/registry layer; identity and
every other chain's path stay untouched. (No rollout/sequence framing — that is the deferred
roadmap.)

### `09-stewardship.md` — Stewardship
**Public-goods governance.** A **Mediolano DAO stewards the commons**. **Zero-fee is a hard
invariant** — no fees in the immutable primitives, no treasury extraction from the substrate.
The DAO's role is neutrality-preservation, parameter and (opt-in, never gating) curation
decisions, and progressive decentralization — **governance without extraction**. Explicitly
distinct from commercial governance models that allocate fee revenue: the substrate has none to
allocate.

### `glossary.md`
Canonical terms: the primitives, identity mechanisms (IP-ID / AccountID / Wallet / Profile),
service & capability vocabulary, CROPS, chain-sovereignty terms, Berne Convention, Integrity
Web. The architecture governs on any conflict.

### `README.md`
Index with reading order, a one-line description of each doc, and the statement that the axioms
(`00`) are the governing authority.

---

## 6. Cross-cutting reframes (the Mediolano signature)

- **Zero-fee is a hard invariant**, not a tunable policy — it is the substrate being a commons
  (Ax 05).
- **Berne-aligned authorship is central** (`05`), framed as durable cross-jurisdiction records
  in immutable content-addressed metadata, never brittle on-chain legal logic.
- **Universality of intelligences is load-bearing** (Ax 08) — human-to-AI from first principles,
  not an "AI agents" feature.
- **No temporal framing** anywhere — foundations only.
- **Stands fully alone** — no commercial layer named; no Medialane.
- **CROPS is expressed and deepened**, never bolted on — it is the same cypherpunk lineage as
  the axioms, stated in another vocabulary.

---

## 7. Out of scope (this pass)

- No contract / SDK / indexer / app changes; **no reading or auditing of `mediolano-contracts`.**
- **No roadmap / trajectory doc** (separate later brainstorm).
- **No formal amendment to the axioms.**
- **No publishing `mediolano-core` public** — that happens when the foundation is finished.
- **No Medialane references.**

---

## 8. Deferred / open questions

- **Roadmap & sequencing** (including any concrete multichain porting order) — later brainstorm.
- **Full formal axiom amendment** — later proposal.
- **The portability *mechanism*** — *how* the identity/provenance graph is made re-anchorable
  (content-addressing, attestation mirroring, cross-chain proofs) is the first real design task
  after this foundation is approved.
- **Grounding `05`/`06`/`07` in the real contract modules** — when contracts are tackled.
