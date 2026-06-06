# How Mediolano Protects IP

*What "protection" really means on Mediolano, and why the proof holds up anywhere. Plain idea
first, then the substance, then links for depth.*

---

Mediolano protects intellectual property by turning a work into a **Berne Convention-compliant
proof of ownership and authorship** — an immutable, timestamped, worldwide-recognized record of who
made a work, when, and under what terms. It performs, permissionlessly and at zero protocol cost,
the proof-of-ownership and registration function that notarial offices and copyright-registration
services traditionally charge significant fees to provide.

## A real proof of ownership

**Tokenizing a work creates a record with genuine legal weight — not a throwaway note.**

When you tokenize a work on Mediolano, you publish it, fix the moment, and bind its license in one
immutable record of authorship and ownership. This is the same function notarial registries and
copyright-registration services provide — and blockchain records of this kind are already
recognized in practice (for example, treated as notarial records in Brazilian court rulings, and
mapped to enforceable licenses by IP protocols such as Story). The claim a Mediolano record makes
is strong and checkable: *this work, this author, this moment, this chain of custody, these terms.*

## Why it's tamper-proof

**The record is anchored to cryptography, not to anyone's goodwill.**

Authorship, ownership, and provenance are written on-chain, where they cannot be silently changed.
The work's details and license live in **content-addressed metadata** (IPFS / Arweave): the
reference is itself the integrity check — it resolves to exactly the bytes that were committed, or
not at all. Nothing in the chain of custody can be rewritten after the fact.

The whole stack is verifiable end to end. There are no hidden backdoors and no privileged party
who can reach in and change a record.

→ Go deeper: [Licensing & Authorship](../architecture/05-licensing-and-authorship.md) ·
[Identity](../architecture/07-identity.md).

## Aligned with the Berne Convention

**Authorship recognized across borders, automatically.**

Mediolano is built to align with the
[Berne Convention](https://en.wikipedia.org/wiki/Berne_Convention) for the Protection of Literary
and Artistic Works — the treaty under which authorship is recognized across more than 180
countries (and, through TRIPS, most WTO members). Berne's core ideas fit the protocol naturally:

- **Automatic protection.** Copyright exists the moment a work is *fixed* — no registration is
  required. A Mediolano record timestamps and anchors that moment.
- **No formalities.** Protection does not depend on registering with an authority; the on-chain
  record stands on its own.
- **National treatment.** A work from one member state is protected in every other member state.
- **Independence of rights.** Protection in each country is independent of the country of origin.

Tokenizing on Mediolano gives a work a durable, portable, Berne-compliant record of authorship and
ownership — recognized wherever the treaty reaches.

## What you get

**A record that outlives platforms and crosses borders.**

Because the proof is immutable, content-addressed, and standard, it is verifiable independently of
any application, marketplace, gateway, or database — and it travels with the creator. Protection
here is not a service that can be switched off; it is a fact anyone can check.

→ Go deeper: [The Integrity Web Axioms](../architecture/00-axioms.md).
