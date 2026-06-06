# How Mediolano Protects IP

*What "protection" really means on Mediolano, and why the proof holds up anywhere. Plain idea
first, then the substance, then links for depth.*

---

Mediolano protects intellectual property by producing **durable, independently verifiable evidence
of authorship** — a permanent record of who made a work, when, and under what terms, that anyone
can check without trusting Mediolano. It does not replace the law; it gives the law something solid
to stand on.

## Evidence, not adjudication

**Mediolano records; courts and jurisdictions adjudicate.**

The protocol does not decide disputes or grant copyright. What it does is create proof that is hard
to fake and impossible to quietly alter — the kind of evidence that strengthens a creator's hand
wherever rights are recognized and enforced. The claim a Mediolano record makes is narrow and
strong: *this work, this author, this moment, this chain of custody.*

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

Mediolano produces the durable, portable evidence that makes those protections easy to assert
wherever the treaty reaches.

## What you get

**A record that outlives platforms and crosses borders.**

Because the proof is immutable, content-addressed, and standard, it is verifiable independently of
any application, marketplace, gateway, or database — and it travels with the creator. Protection
here is not a service that can be switched off; it is a fact anyone can check.

→ Go deeper: [The Integrity Web Axioms](../architecture/00-axioms.md).
