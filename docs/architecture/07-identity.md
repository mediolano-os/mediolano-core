# 07 — Identity

**Authority:** the [Integrity Web Axioms](00-axioms.md) govern; where this document conflicts
with them, the axioms win.

Every identity is self-sovereign (Axiom 04). The substrate gives works and actors stable
identities that they own, that no external party can revoke, and that survive the loss of any
single chain.

---

## Self-sovereign by default

An identity's root is its own — not a username granted by a platform, not an address blessed by a
gatekeeper. Wallets, keys, and logins **attach** to an identity; the identity does not depend on
any one of them. This is the protocol-level expression of Axiom 04: *every identity is
self-sovereign.*

## Account facets

An Account ([02 — Core Model](02-core-model.md)) is seen through three facets:

- **Wallet** — a specific address on a specific chain, `(chain, address)`. The only thing that can
  sign and act on-chain. A wallet is *how* an Account acts, not *who* it is.
- **Account** — the logical actor, identified by its `AccountID` (below). It holds the actor's
  roles and history; wallets, keys, and logins attach to it, and **none is required as a gate** —
  an actor without a wallet is still a first-class Account.
- **Profile** — off-chain enrichment (display name, bio, avatar). Editable, never authoritative;
  losing it loses no protocol state.

## Two cross-chain mechanisms, never conflated

Identity spans chains through two distinct mechanisms that must never be confused:

- **`IP-ID`** — the **work** identifier. It lets the same logical work, represented on several
  chains, be provably "the same work." It relates *Assets* ([02](02-core-model.md)).
- **`AccountID`** — the **actor** identifier. It lets the same actor, holding wallets across
  several chains, be provably "the same actor," linked through a verifiable signed-attestation
  graph. It relates *Accounts*.

Assets use `IP-ID`; Accounts use `AccountID`. One is about works, the other about actors; they are
never collapsed into one mechanism.

## Universality of intelligences

Identity makes no distinction between forms of intelligence (Axiom 08). Humans, AI agents,
organizations, and future intelligences hold identities and participate on the same terms. There
are no human-only flows, no anti-agent measures, and no interaction requirements an agent cannot
satisfy ([01 §7](01-principles.md)). An identity is defined by what it can prove and sign, not by
what kind of intelligence stands behind it.

## Portable and re-anchorable

Identity and the work-to-actor provenance graph must be **portable** and **re-anchorable** so they
survive any substrate change ([01 §9](01-principles.md), [08 — Chain Sovereignty](08-chain-sovereignty.md)).
Identity may be anchored on the best-available prover, but it is never *solely kept* there: the
canonical identity and its provenance must be reconstructible elsewhere, so no chain's failure can
strand who an actor is or what a work is.

> The concrete mechanism for making the identity/provenance graph re-anchorable —
> content-addressing, attestation mirroring, cross-chain proofs — is the first real design task
> after this foundation, addressed separately.
