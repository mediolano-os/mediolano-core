# 05 — Licensing & Authorship

**Authority:** the [Integrity Web Axioms](00-axioms.md) govern; where this document conflicts
with them, the axioms win.

This is the heart of what Mediolano protects. Creativity is integrity (Axiom 09): a work's
authorship, ownership, and rights must be recorded so durably and so verifiably that they hold up
independently of any application, marketplace, gateway, or database — and across jurisdictions.

---

## Berne-aligned authorship

Tokenizing a work on Mediolano creates a **Berne Convention-compliant record of authorship and
ownership** — a timestamped, immutable proof and licensing record recognized across the
[Berne Convention](https://en.wikipedia.org/wiki/Berne_Convention)'s 180+ member states. It
performs, on-chain, permissionlessly, and at zero protocol cost, the proof-of-ownership,
publication, and licensing function that notarial offices and copyright-registration services
traditionally charge significant fees to provide.

The claim a Mediolano record makes is strong and checkable: *this work, this author, this moment,
this chain of custody, these terms* — tamper-proof, content-addressed, and verifiable by anyone,
forever (Axiom 04, Axiom 09).

## Durable records: immutable and content-addressed

Authorship, ownership, and license claims live in **immutable, content-addressed metadata** —
IPFS or Arweave documents referenced from the token. Content addressing means the reference *is*
the integrity check: the pointer resolves to exactly the bytes that were committed, or it does
not resolve at all. Nothing in the chain of custody can be quietly rewritten.

This is why durability is a metadata-and-content-addressing property rather than a contract
feature: the record must outlive any single contract, client, or gateway.

## Programmable, metadata-first licensing

A License is the programmable set of rights governing how an Asset may be used, copied, modified,
and monetized. It is encoded as standard, OpenSea-compatible metadata attributes
([04 — Interoperability](04-interoperability.md)) and is a *view* on the Asset's metadata, not a
separate entity ([02 — Core Model](02-core-model.md)). Licenses travel with the Asset and remain
readable by wallets, marketplaces, indexers, SDKs, and agents.

## Soft-enforced by default; selective on-chain enforcement

By default, licensing is **declared, not enforced on-chain**: a contract does not revert because
a derivative was made or a term was ignored. Enforcement is selective and happens at the
application or partner layer, which can interpret terms per context and per jurisdiction.

Contracts enforce **only** the specific rules they explicitly implement — and only where a
service genuinely needs it: royalty splits on settlement, escrow for negotiated deals, time-locks
for delayed disclosure, access checks for gated entitlements. These are opt-in service behaviors,
never a default tax on every asset ([01 §6](01-principles.md)).

## Why no brittle on-chain legal logic

Contracts are immutable; law is not. Intellectual-property rules change over time and differ
sharply between jurisdictions. Hardcoding legal enforcement into an immutable contract would age
badly and fragment by territory — a contract written to one jurisdiction's rules would
mis-enforce in another, with no way to correct it.

So the substrate keeps the two concerns apart:

- **Durable records** — authorship, ownership, license terms — live on-chain and in immutable
  content-addressed metadata, where permanence is the point.
- **Enforcement** — the interpretation and application of those terms — stays selective and at the
  application layer, where it can adapt to law and context without rewriting the record.

This keeps the primitives simple, durable, and neutral, while letting the ecosystem above them
enforce as richly and as locally as each jurisdiction requires.
