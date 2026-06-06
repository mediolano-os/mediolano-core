# 04 — Interoperability

**Authority:** the [Integrity Web Axioms](00-axioms.md) govern; where this document conflicts
with them, the axioms win.

Mediolano's reach comes from standards, not from lock-in. An asset created through the substrate
must remain usable and understandable far outside any single application.

---

## Standard token interfaces

Assets follow standard token interfaces — ERC-721 and ERC-1155 on chains that support them, and
the closest equivalent on chains that do not. Standard interfaces mean third-party wallets,
marketplaces, indexers, and agents already know how to read and move a Mediolano asset.

## A standard metadata envelope

Metadata follows the widely-adopted, OpenSea-compatible baseline:

- `name`
- `description`
- `image`
- `animation_url` (when useful)
- `external_url` (when useful)
- `attributes`

Protocol-specific information — license terms, authorship claims, service data — **extends** this
baseline through additional attributes and content-addressed references. It never **replaces** it.
A consumer that understands only the baseline still sees a coherent asset.

## Interoperability is the anti-lock-in moat

Because assets speak standard interfaces and carry standard metadata, they travel with the
creator and remain tradeable and renderable on surfaces the substrate has never heard of
([01 §5](01-principles.md)). This is deliberate: interoperability is a strength, not a leak. The
substrate's value is in the durability and verifiability of what it records, not in trapping the
records inside it.

**Rules out:**
- Contract behaviors that trap assets — mandatory hooks that fail on third-party surfaces, or
  non-transferable-by-default — except where a specific service genuinely requires it (and says
  so).
- Metadata that only a Mediolano-specific client can interpret.
