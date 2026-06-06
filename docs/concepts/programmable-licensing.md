# Programmable Licensing

*How rights work on Mediolano: terms you set, encoded in the asset itself, readable by anyone —
human or machine. Plain idea first, then substance, then links for depth.*

---

A Mediolano license is not a document filed somewhere else — it is **programmable metadata that
lives on the asset and travels with it everywhere it goes.** You decide the terms; the asset
carries them; wallets, marketplaces, indexers, and AI agents can all read them.

## Licenses as portable metadata

**The terms ride along with the work.**

License terms are encoded as standard, machine-readable attributes on the asset. Anything that
understands the standard token format understands the license — so the rights are legible far
outside any Mediolano-specific interface, and they cannot be separated from the work they govern.

## Immutable proof at mint

**The terms are fixed at creation and can't be quietly rewritten.**

When a work is tokenized, its license is committed alongside it in immutable, content-addressed
metadata. That creates a permanent proof of exactly what terms applied at the moment of creation —
a reference point no one can alter after the fact.

## The creator chooses

**You pick the license; the protocol pins no default on you.**

Licensing is Creative-Commons-compatible, so creators can express clear, human-readable terms —
from fully open dedications like **CC0** to attribution and share-alike terms like **CC BY** and
**CC BY-SA**. Mediolano does not impose a single protocol-wide default: the choice belongs to the
creator, and custom terms are possible.

## Soft-enforced by default

**Terms are declared; enforcement is selective.**

By default a license *declares* the rights — a contract does not revert because someone made a
derivative. Enforcement happens selectively, at the application or service layer, and on-chain only
where a specific service genuinely needs it (royalty splits, escrow, time-locks, access checks).
This keeps the primitives simple and durable while letting the ecosystem above them enforce as
richly as each context requires.

→ Go deeper: [Licensing & Authorship](../architecture/05-licensing-and-authorship.md) ·
[Interoperability](../architecture/04-interoperability.md).

## Remix and derivatives

**Rights propagate to the works built on top.**

Because terms are machine-readable and travel with the asset, derivatives can honor the parent's
license by construction:

- **Attribution preserved** — metadata pointers keep the original creator credited.
- **Share-alike propagates** — if the parent is ShareAlike, the derivative must be too.
- **Commercial limits inherit** — if the parent forbids commercial use, the derivative cannot grant
  it.

→ Go deeper: [Service Model](../architecture/06-service-model.md).

## Readable by every intelligence

**Agents can verify rights before they act.**

Because licenses are structured and on-chain, an AI agent can scan for works with compatible terms,
verify what it is allowed to do, generate a derivative, and mint it with the source correctly
linked — all autonomously, and all while honoring the original terms. Rights that machines can read
are rights machines can respect.
