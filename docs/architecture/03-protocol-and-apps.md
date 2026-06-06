# 03 — Protocol & Applications

**Authority:** the [Integrity Web Axioms](00-axioms.md) govern; where this document conflicts
with them, the axioms win.

Mediolano is a **neutral substrate**. Applications, indexers, SDKs, and agents are consumers of
it. This document draws the line between the two: what carries authority and what merely presents
it.

---

## What lives where

**On-chain — authority.** Ownership, balances, mint authority, provenance, order state, service
records, and emitted events live on-chain. This is the only source of truth
([01 §1](01-principles.md)).

**Off-chain — caches and views.** Indexes, search, aggregation, reputation rollups, and profiles
live off-chain. They exist for discovery and presentation and are **rebuildable from chain
events** ([02 — Core Model](02-core-model.md)). Losing them loses no protocol state.

## Consumers present, they do not authorize

An application renders a view of on-chain reality. An indexer caches it. An SDK exposes it. An
agent consumes it. None of them authorizes a protocol action, and none may gate a protocol action
on off-chain state — if the contract accepts a call, the action is valid.

The substrate stays fully functional if any single consumer disappears. A frontend going dark, an
indexer halting, or a gateway failing changes nothing about what is true on-chain
([01 §11](01-principles.md)).

## No privileged interfaces

There are no private interfaces reserved for a blessed client. Anything one consumer can do, any
consumer can do — including AI agents, which participate on the same terms as any other actor
([01 §7](01-principles.md), [01 §11](01-principles.md)). The substrate exposes one surface; the
diversity of clients is a property of openness, not of permission.

## Why this split

Keeping authority on-chain and presentation off-chain is what makes the substrate a public good:
it can be indexed, forked, and re-clienteled by anyone without asking, and it cannot be captured
by whoever happens to run the most popular interface. The protocol is the commons; the
applications are tools that consume it.
