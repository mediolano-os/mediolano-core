# Glossary

Canonical terms used across this architecture. Where a term is defined more fully, the source doc
is linked. Where anything here conflicts with `architecture/`, the architecture governs.

---

## The primitives

- **Asset** — A unit of intellectual property tokenized on a chain, held by an Account, carrying
  its License in metadata. Identified chain-locally by `(chain, contractAddress, tokenId)`. Not a
  database row, not bound to any application, not the same as its representations on other chains.
  [02 — Core Model](architecture/02-core-model.md)
- **Account** — The actor: a human, AI agent, organization, or collector. The umbrella for
  everyone and everything that acts. Identified by its `AccountID`.
  [02](architecture/02-core-model.md), [07](architecture/07-identity.md)
- **Service** — A protocol module that produces Assets or matches Orders (or both), identified by
  a stable string ID and declaring typed capabilities. The substrate grows by *adding* services.
  [02](architecture/02-core-model.md), [06](architecture/06-service-model.md)
- **License** — The programmable rights governing how an Asset may be used, copied, modified, and
  monetized. A *view* on the Asset's metadata, not a separate entity.
  [02](architecture/02-core-model.md), [05](architecture/05-licensing-and-authorship.md)
- **Order** — A signed proposal to exchange Assets. Settles on the chain it was posted on.
  [02](architecture/02-core-model.md)
- **Event** — An on-chain occurrence indexers consume. A primitive because an indexer's worldview
  is built from events. [02](architecture/02-core-model.md)

## Identity

- **Wallet** — A specific address on a specific chain, `(chain, address)`. The only thing that can
  sign and act on-chain — *how* an Account acts, not *who* it is.
  [07](architecture/07-identity.md)
- **AccountID** — An Account's own root identifier. Wallets, keys, and logins attach to it; none is
  required as a gate. Links the same actor's wallets across chains via a signed-attestation graph.
  [07](architecture/07-identity.md)
- **IP-ID** — A canonical *work* identifier. Lets the same work, represented across chains, be
  provably "the same work." [07](architecture/07-identity.md)
- **Profile** — Off-chain enrichment (display name, bio, avatar). Editable, never authoritative;
  losing it loses no protocol state. [07](architecture/07-identity.md)
- **Self-sovereign identity** — An identity rooted in itself, not granted or revocable by any
  external party. [07](architecture/07-identity.md)

## Services & licensing

- **Capability** — A typed affordance a Service declares (e.g. `mint`, `list`, `buy`, `license`,
  `remix`, `claim`, `airdrop`, `escrow`). Needing behavior outside the set is a signal to expand
  the set, not to go free-form. [06](architecture/06-service-model.md)
- **Service registry / discovery** — The discoverable catalog of services, keyed by stable IDs, so
  any consumer can find and use them uniformly. [06](architecture/06-service-model.md)
- **Soft enforcement** — The default: a License *declares* terms; the contract does not revert on a
  derivative. Enforcement is selective and at the application layer. Selective on-chain enforcement
  (royalty splits, escrow, time-locks, access checks) exists only where a service requires it.
  [05](architecture/05-licensing-and-authorship.md)
- **Content-addressed metadata** — Authorship, ownership, and license records stored on IPFS /
  Arweave and referenced from the token, where the reference is itself the integrity check.
  [05](architecture/05-licensing-and-authorship.md)

## Chain sovereignty

- **Prover/settlement role** — The function that roots verifiable trust and settlement, filled
  behind an interface so it can be re-homed to another chain without rewriting consumers.
  [08](architecture/08-chain-sovereignty.md)
- **Portability boundary** — The line between what must survive losing a chain (identity,
  provenance, exit) and what may be chain-local (a venue contract, an open order, that chain's
  native assets). [08](architecture/08-chain-sovereignty.md)
- **Exit** — A participant's guaranteed ability to move identity and assets off any chain the
  substrate uses. [08](architecture/08-chain-sovereignty.md)
- **Litmus test** — Adding a chain touches only an adapter/registry layer; identity and every other
  chain's path stay untouched. [08](architecture/08-chain-sovereignty.md)
- **Prove without revealing** — Using zero-knowledge to prove a claim without exposing the data
  behind it; how verifiability and privacy are reconciled.
  [08](architecture/08-chain-sovereignty.md)

## Frameworks & concepts

- **CROPS** — Censorship-resistance, Open-source, Privacy, Security; a cypherpunk values framework
  emphasizing "longevity over breadth." Expressed in [01](architecture/01-principles.md), deepened
  in [08](architecture/08-chain-sovereignty.md).
- **Berne Convention** — The treaty for the Protection of Literary and Artistic Works (180+
  countries), the standard Mediolano's durable authorship records are designed to align with.
  [05](architecture/05-licensing-and-authorship.md)
- **Integrity Web** — The foundational frame Mediolano serves; its
  [Axioms](architecture/00-axioms.md) are the governing authority of this architecture.
- **Mediolano** — The public-goods intellectual-property tokenization substrate of the Integrity
  Web: permissionless, zero-fee, immutable, interoperable, multichain, and open to all
  intelligences. [01](architecture/01-principles.md)
- **Universality of intelligences** — Humans, AI agents, organizations, and future intelligences
  participate on equal terms (Axiom 08). [07](architecture/07-identity.md)
