# How Mediolano Works

*The life of an intellectual-property asset on Mediolano — from a work in your hands to a
permanent, usable record anyone can verify. Read the first line of each step for the idea; follow
the links to go deeper.*

---

A work becomes a Mediolano asset in one move and stays useful forever. You tokenize it, the proof
of authorship lives on-chain and in permanent storage, the license travels with it, and from there
it can be transferred, traded, remixed, or built upon — all without asking anyone's permission and
without the protocol taking a cut.

## 1. Tokenize

**You mint a record of your work: who made it, what it is, and when.**

Tokenizing creates a standard on-chain asset that represents your intellectual property. The act
of minting writes an authorship and ownership record that did not exist before — a starting point
for everything that follows. Anyone can mint; there is no allowlist and no gatekeeper.

## 2. Protect

**The proof is immutable and content-addressed, so it cannot be quietly changed or lost.**

The work's details and claims live in **content-addressed metadata** (IPFS / Arweave) referenced
from the asset — the reference is itself an integrity check: it resolves to exactly what was
committed, or not at all. Ownership and provenance live on-chain, where they are tamper-proof.
Because the record does not depend on any one company, gateway, or database, it survives them.

→ Go deeper: [How Mediolano protects IP](ip-protection.md).

## 3. License

**You attach programmable terms that travel with the asset.**

A license is encoded as standard metadata on the asset, so it is readable by wallets,
marketplaces, indexers, and agents wherever the asset goes. Terms are declared by default and
enforced selectively — only where a specific service genuinely needs on-chain enforcement (such as
royalty splits or escrow). The creator chooses the terms.

→ Go deeper: [Programmable licensing](programmable-licensing.md).

## 4. Use & compose

**The asset plugs into a growing set of services.**

Once an asset exists, it can be transferred, traded, remixed into derivative works, gated for
access, or wired into revenue sharing — each of these is a **service**, a self-contained module
that anyone can build on. Mediolano grows by *adding* services, never by changing the ones already
deployed, so an asset behaves the same way tomorrow as it does the day it was minted.

→ Go deeper: [Service Model](../architecture/06-service-model.md).

## 5. Protocol, not app

**The chain is the source of truth; apps present it but never authorize it.**

Mediolano is neutral infrastructure. Applications, indexers, and interfaces render and organize
on-chain reality, but they never become the authority over it, and the protocol keeps working even
if any single one of them disappears. The primitives have **no admin, no owner, and no upgrade
switch** — no one can change the rules under a record already made — and they are **zero-fee**: the
substrate takes nothing. It is also not bound to any single chain; chains are peers, and your
identity and work are designed to outlive any of them.

→ Go deeper: [Core Model](../architecture/02-core-model.md) ·
[Protocol & Applications](../architecture/03-protocol-and-apps.md) ·
[Licensing & Authorship](../architecture/05-licensing-and-authorship.md).
