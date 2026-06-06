# 06 — Service Model

**Authority:** the [Integrity Web Axioms](00-axioms.md) govern; where this document conflicts
with them, the axioms win.

The substrate is not a fixed feature set. It is a small core of primitives plus an open, growing
set of **services**. This document describes how the substrate grows.

---

## Grow by adding, not editing

The central commitment: **the substrate grows by adding services, not by editing them.** Existing
services are immutable ([01 §3](01-principles.md)); new capability arrives as a new service with a
new stable ID. Nothing already deployed changes meaning when the substrate expands.

## What a Service is

A **Service** is a protocol module that produces Assets, matches Orders, or both
([02 — Core Model](02-core-model.md)). It is identified by a stable string ID and declares the
typed **capabilities** it offers. Consumers route by the service ID; they never infer behavior by
string-comparing addresses.

## Capabilities are typed

A capability is a named affordance a service declares — for example: `mint`, `list`, `buy`,
`make_offer`, `cancel`, `transfer`, `license`, `remix`, `claim`, `airdrop`, `escrow`,
`subscribe`. The set is deliberately typed and shared: needing behavior outside it is a signal to
*expand the set*, not to invent free-form, unrecognizable actions. A shared capability vocabulary
is what lets wallets, indexers, SDKs, and agents discover and use any service uniformly
([01 §7](01-principles.md), [01 §11](01-principles.md)).

## Marketplaces are services, not a special layer

Order-matching surfaces — marketplaces, auctions, escrows — are **services like any other**. They
declare order-matching capabilities and route the same way every other service does. There is no
privileged commercial "venue" layer, and there is **no fee logic in the substrate**
([01 §4](01-principles.md)). Economic models are something applications build *around* the
substrate, not into it.

## Discovery

Because every service has a stable ID and a typed capability set, the catalog of services is
discoverable by any consumer — human, application, or agent — on equal terms. Discovery is a
property of the open substrate, not a curated list anyone controls.

---

> The concrete families of service contracts, their interfaces, and their on-chain shapes are
> documented when the contracts themselves are addressed — a separate effort, out of scope for
> this foundation.
