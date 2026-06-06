# 01 — Principles

**Authority:** the [Integrity Web Axioms](00-axioms.md) govern; where this document conflicts
with them, the axioms win.

The load-bearing principles of Mediolano, each derived from the axioms. They constrain every
design choice for the substrate — what gets stored where, what is gated by what, what is
discoverable to whom. When two design considerations conflict, the principle wins. When a
principle is in tension with an axiom, the axiom wins.

This is not a coding style guide. It is the set of architectural commitments the rest of this
documentation builds on.

---

## The principles

### 1. The contract is the only truth

Mediolano is the on-chain state and the contracts that govern it. Indexers, SDKs, and
applications are caches and views for discovery, search, and aggregation. Authority lives in the
contract: if the contract accepts a call, it is valid.

**Roots:** Axioms 01, 02, 04.

**Rules out:**
- Gating user actions (mint, transfer, trade) on off-chain state.
- "Soft state" that cannot be rebuilt from chain events.
- Any cache or moderation surface that contradicts on-chain reality.

### 2. Permissionless & censorship-resistant

Anyone can use the substrate without asking. Anyone can deploy a contract that integrates with
it, index it, or build a competing client. No party stands between a participant and a protocol
action.

**Roots:** Axioms 03, 07, 10.

**Rules out:**
- Allowlists for who may create, mint, list, or trade.
- Approval workflows over legitimate protocol actions.
- Hardcoded curation of which contracts the substrate "respects."

### 3. Immutable primitives

The primitives are fully immutable: no admin, no owner, no upgrade path, no setters. They evolve
by **redeploy**, not by mutation. A record made under a primitive cannot be silently changed by
anyone, including its authors.

**Roots:** Axioms 04, 01.

**Rules out:**
- Owner/admin keys or upgradeable proxies over public-goods primitives.
- Mutable parameters that could re-write the meaning of existing records.

### 4. Zero-fee public-goods substrate

The tokenization and protection primitives charge nothing. The infrastructure is a commons; a
fee inside an immutable public-goods primitive would both gate a permissionless action and freeze
fee policy into code. Applications may build their own economic models around the substrate; the
substrate itself stays neutral and free.

**Roots:** Axiom 05.

**Rules out:**
- Any fee taken by the primitives themselves.
- Coupling protection or ownership records to a payment.

### 5. Interoperability over lock-in

Assets use standard token interfaces and a standard metadata envelope. A Mediolano asset is
usable and understandable outside any single application — it travels with its creator and
survives the disappearance of any one interface.

**Roots:** Axioms 03, 05, 09.

**Rules out:**
- Contract behaviors that trap assets (hooks that fail on third-party surfaces,
  non-transferable-by-default) except where a specific service genuinely requires it.
- Metadata that only a Mediolano-specific client can read.

### 6. Durable, Berne-aligned authorship & licensing

Authorship, ownership, and license claims live in immutable, content-addressed metadata so they
are verifiable independently of any application, across jurisdictions. Licensing is
metadata-first and **soft-enforced by default**: contracts enforce only the specific rules they
explicitly implement (escrow, royalty splits, time-locks, access checks).

**Roots:** Axioms 09, 04.

**Rules out:**
- Brittle on-chain legal logic baked into immutable contracts.
- Treating durable authorship/ownership metadata as optional or mutable.

### 7. Universality of intelligences

Humans, AI agents, organizations, and future intelligences are equal, first-class participants.
The substrate serves all forms of intelligence on the same terms.

**Roots:** Axioms 08, 05.

**Rules out:**
- Human-only flows, anti-agent measures, or interaction requirements no agent can satisfy.
- Different treatment of participants by category at the protocol level.

### 8. Privacy is sovereignty

Participants prove what they must without revealing what they need not — **prove without
revealing**. The substrate keeps zero-knowledge a possibility everywhere and minimizes the data
any layer stores. Data not held cannot be compelled.

**Roots:** Axiom 06.

**Rules out:**
- Surfaces that *require* disclosure where a proof would suffice (forced wallet-graph linkage,
  mandatory holder identity).
- Accreting personal data the substrate does not need.

### 9. Chain sovereignty

Verifiable trust is a **role, not a place**. Identity and provenance are portable and
re-anchorable; no single chain is an existential dependency; participants always retain an exit.
Chain is a first-class dimension everywhere, never an assumption.

**Roots:** Axioms 07, 02, 04.

**Rules out:**
- Treating any one chain as the permanent foundation.
- Identity or provenance that cannot survive a substrate change.

### 10. Self-sovereign identity

Every identity is self-sovereign. An actor's identity is its own root; wallets, keys, and logins
**attach** to it, and none is required as a gate. Losing an off-chain enrichment loses no
protocol state.

**Roots:** Axioms 04, 06.

**Rules out:**
- One-wallet-equals-one-identity assumptions.
- Identity that an external party can revoke.

### 11. Neutral, open, forkable substrate

The substrate is neutral public infrastructure. Anyone can index it, fork it, or build a
competing client. It stays useful even if any single frontend, indexer, gateway, or venue
disappears.

**Roots:** Axioms 03, 05, 07.

**Rules out:**
- Privileged, private interfaces available only to a blessed client.
- Designs that make a single application indispensable to the protocol.

---

## CROPS

These principles express the cypherpunk values shared with the broader ecosystem — the same
lineage as the axioms, stated in another vocabulary:

| | Where it lives |
|---|---|
| **C**ensorship-resistance | Principles 2, 9 |
| **O**pen-source | Principle 11 |
| **P**rivacy | Principle 8 |
| **S**ecurity | Principles 1, 3 |

The throughline is **longevity over breadth**: survive the loss of any single chain, keep the
foundations clean, and resist feature-breadth that paints the substrate into a corner. CROPS is
expressed here and deepened in [08 — Chain Sovereignty](08-chain-sovereignty.md).

---

## How to use this document

When designing a service, schema, or feature, walk the principles. If a design conflicts with
one, either change the design until it complies, or argue that the principle should change — and
amend this document by consensus, ultimately deferring to the [axioms](00-axioms.md). A design
that violates a principle without amending the document is, by definition, a regression.
