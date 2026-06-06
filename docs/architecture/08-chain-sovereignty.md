# 08 — Chain Sovereignty

**Authority:** the [Integrity Web Axioms](00-axioms.md) govern; where this document conflicts
with them, the axioms win.

Decentralization is resilience (Axiom 07). A substrate meant to hold authorship and ownership
*forever* cannot bet its existence on any one chain. This document states what must be true so
that the substrate, and everyone who uses it, survives the loss of any single chain — including
the best one available.

---

## No chain is the foundation

Chain is a **first-class dimension** everywhere in the model — never dropped, never assumed
([02 — Core Model](02-core-model.md)). The chains the substrate lives on are **peers**: Starknet,
Ethereum, and Solana stand on equal footing, and the set is open-ended for others. No chain is
privileged as the home of the substrate; the substrate is defined independently of any of them.

## Verifiable trust is a role, not a place

The substrate needs two properties from a chain: **verifiability** (the ability to *prove*
identity, provenance, and settlement) and **censorship-resistance** (so neither users nor the
substrate can be shut out). These are filled by **roles behind interfaces**, not by hardcoded
chain identities:

- a **prover/settlement role**, rooted on the best-available proving system, reachable through a
  boundary that can be re-homed to another chain without rewriting consumers;
- a **censorship-resistant settlement root**, the most credibly neutral place of last resort.

Because they are roles, a chain can fill one without becoming an existential dependency, and the
role can migrate without stranding anyone.

## Realize the protocol by porting its own primitives

The substrate extends to a new chain by **porting Mediolano's own primitives onto that chain** —
not by routing commerce through external venues it does not control. Owning the primitives on each
chain is what keeps the substrate neutral and uncapturable; renting someone else's venue would
import a dependency the substrate cannot govern ([01 §11](01-principles.md)).

Reading the world is different from depending on it: **external assets on any chain are freely
indexed and surfaced.** Indexing the broader world is welcome; routing authority through contracts
the substrate does not control is not.

## The portability boundary

"Survive losing a chain" does not mean keeping that chain's assets — it means keeping *who you are
and what you made*:

- **Must survive any chain dying** — identity and the work-to-actor provenance graph (`IP-ID`,
  `AccountID`, attestations; see [07 — Identity](07-identity.md)), and every participant's ability
  to **exit**. These are anchored on the current best prover but never *solely kept* there.
- **May be chain-local** — a venue contract, an open order, and assets that only ever lived on the
  chain that died. Commerce is inherently per-chain; an order on a dead chain is simply gone, and
  that is correct.

So the precise guarantee: if a chain disappears, participants keep their identity, their
provenance, and a path out — they do not keep that chain's native assets, and the substrate does
not pretend they could.

## Users always retain an exit

Sovereignty means a participant can always move identity and assets off any chain the substrate
uses. Any design that traps a participant on one chain violates the core
([01 §9](01-principles.md)).

## Privacy is a duty of the prover

The same zero-knowledge substrate that delivers verifiability must equally serve **privacy**
(Axiom 06). Verifiability and privacy are not opposites; zero-knowledge reconciles them: **prove a
claim without revealing the data behind it.** A creator proves authorship without exposing their
wallet graph; a holder proves entitlement without revealing who they are; provenance is verifiable
without the whole graph being public.

So privacy is not a separate system bolted on — it is a second duty of the prover role defined
above ([01 §8](01-principles.md)). Surfaces must not *require* disclosure where a proof would do,
and the substrate minimizes the data any layer stores.

## CROPS

This document is where the cypherpunk values from [01 — Principles](01-principles.md) are deepest:

- **C**ensorship-resistance — the entire survival-and-exit thesis above.
- **O**pen-source — neutral primitives anyone can index, fork, or re-client.
- **P**rivacy — the prover's second duty, prove-without-revealing.
- **S**ecurity — immutable primitives and proof-rooted trust.

The throughline is **longevity over breadth**: survive the loss of any chain, keep the foundation
clean, do not paint the substrate into a corner.

## Litmus test

A single check tells you whether a change still honors chain sovereignty:

> **Adding a chain touches only an adapter/registry layer — identity, provenance, and every
> already-supported chain's path stay untouched.**

If adding a chain would force a change to the identity model or to another chain's path, the seam
is in the wrong place.

---

> Sequencing — which chains, in which order, and the status of any port — is not an architectural
> concern. It belongs to a separate roadmap effort, deliberately out of scope for this foundation.
