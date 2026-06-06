# 02 — Core Model

**Authority:** the [Integrity Web Axioms](00-axioms.md) govern; where this document conflicts
with them, the axioms win.

The irreducible primitives of the Mediolano substrate. Everything else — every role, view,
attribute, or cache — is built from these. Each primitive is defined by *what it is*, *its
identity*, and *what it is not*.

---

## Asset

**What it is.** A unit of intellectual property tokenized on a chain, held by an Account,
carrying its License in metadata. An Asset is the on-chain representation of a creative work:
authorship, ownership, and rights claims attach to it.

**Identity.** Chain-locally `(chain, contractAddress, tokenId)`. The same logical *work* may have
representations on several chains; relating them is the job of `IP-ID` (see
[07 — Identity](07-identity.md)).

**What it is not.** Not a database row (the database is a cache). Not bound to any application —
externally-created assets are first-class. Not the same thing as its representations on other
chains.

## Account

**What it is.** The actor: a human, an AI agent, an organization, or a collector. The umbrella
for everyone and everything that acts on the substrate.

**Identity.** Its own `AccountID` (see [07](07-identity.md)) is the root of identity. Wallets,
keys, and logins attach to it; an Account needs no single wallet to exist.

**What it is not.** Not a wallet (a wallet is *how* an Account acts, not *who* it is). Not a
profile (a profile is editable enrichment, never authoritative).

## Service

**What it is.** A protocol module that produces Assets, matches Orders, or both — identified by a
stable string ID and declaring typed capabilities. The substrate grows by *adding* services, not
by editing them (see [06 — Service Model](06-service-model.md)).

**Identity.** Its stable service ID. Consumers route by the ID, never by string-comparing
addresses.

**What it is not.** Not editable in place (immutability, [01 §3](01-principles.md)). Not a
privileged or blessed set — anyone may add a service.

## License

**What it is.** The programmable rights governing how an Asset may be used, copied, modified, and
monetized. Encoded as standard metadata attributes and travelling with the Asset (see
[05 — Licensing & Authorship](05-licensing-and-authorship.md)).

**Identity.** None of its own — a License is a *view* on an Asset's metadata.

**What it is not.** Not a separate entity. Not, by default, on-chain-enforced — enforcement is
selective and lives at the service or application layer.

## Order

**What it is.** A signed proposal to exchange Assets (offer against consideration). Matched and
settled by a Service with order-matching capabilities.

**Identity.** Its order hash. An Order settles on the chain it was posted on.

**What it is not.** Not cross-chain by itself. Not authoritative until it settles on-chain — an
unsettled order is a proposal, not state.

## Event

**What it is.** An on-chain occurrence that indexers consume — a mint, a transfer, a settlement,
a service action. A primitive because an indexer's entire worldview is reconstructed from events.

**Identity.** Its on-chain emission (transaction, log index).

**What it is not.** Not authoritative state in itself — the chain's state is authoritative; events
are the stream from which caches are built.

---

## Roles are attributes, never primitives

`creator`, `collector`, `agent`, and `organization` are **attributes of an Account**, not
primitives. A role may gate an application's *affordances* (authoring tools, dashboards), but a
role **never gates a protocol action**: any Account that owns an Asset can act on it
([01 §2](01-principles.md), [01 §7](01-principles.md)). "Creator" in particular is a role, not an
entity — the primitive is always **Account**.
