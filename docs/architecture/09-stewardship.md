# 09 — Stewardship

**Authority:** the [Integrity Web Axioms](00-axioms.md) govern; where this document conflicts
with them, the axioms win.

Public goods are sacred (Axiom 05). A commons needs tending, but tending must never become owning.
This document describes how Mediolano is stewarded without being captured.

---

## A DAO stewards the commons

Mediolano is stewarded by a **DAO** whose role is to keep the substrate neutral, open, and
durable. Stewardship is custodial, not proprietary: the DAO tends the commons on behalf of
everyone who uses it, and holds no privileged power over the immutable primitives themselves
([01 §3](01-principles.md)).

## Zero-fee is a hard invariant

The substrate's tokenization and protection primitives are **zero-fee** — a hard invariant, not a
tunable parameter ([01 §4](01-principles.md)). There is no fee inside the primitives and no
treasury extraction from the substrate. This is a direct consequence of Axiom 05: infrastructure
that belongs to everyone cannot meter the people it belongs to.

This is the sharp line between stewardship of a public good and commercial governance: a
commercial protocol governs how it *allocates* the fees it collects; Mediolano has **none to
allocate**, because it collects none. Applications may build economic models *around* the
substrate; the substrate stays free.

## Governance without extraction

What the DAO does govern is **neutrality and resilience**, never gates and never rents:

- parameter and curation decisions that are **opt-in and never become gates** on protocol actions
  ([01 §2](01-principles.md));
- the integrity of the commons — proof systems, identity registries, and tokenization primitives
  kept open and uncapturable (Axiom 05);
- **progressive decentralization** of stewardship itself, so the commons depends on no single
  steward over time (Axiom 07).

## A public good, in the open

The substrate and its supporting design are public infrastructure. The proof systems, identity
registries, and tokenization protocols are commons in the full sense of Axiom 05 — open to be
read, audited, indexed, forked, and built upon by anyone.

> `mediolano-core` itself is published openly once this foundation is complete — making the
> architecture of the commons as public as the commons it describes.

## Rules out

- Turning stewardship into ownership of, or a backdoor into, the immutable primitives.
- Any fee, rent, or extraction taken by the substrate.
- Curation or parameters that harden into gates on permissionless actions.
- A permanent, irreplaceable steward.
