# Mediolano Documentation — Guides Slice — Design Spec

**Date:** 2026-06-06
**Status:** Draft for review.
**Repo:** `mediolano-core` (documentation only). Fully public once complete.
**Scope:** **Slice 5** (final) of the documentation program — a protocol-level developer guide,
with the app-usage guides kept app-side. Governing program context:
`2026-06-06-mediolano-docs-vision-design.md`.

---

## 1. Goal

Give builders a clear, principle-level entry point for building on Mediolano, while keeping the
protocol core clean — app usage/setup docs stay with the app.

---

## 2. Decision locked in brainstorming

**Revises the Slice-1 "bring app guides into core" call.** Per the sharpened "framework, not
finality" scope:
- `mediolano-core` gets **one** protocol-level developer guide (`guides/build-on-mediolano.md`).
- `dapp-guide`, `user-guide`, `permissionless-setup` (legacy) are **app-specific** and **stay in the
  app repo** (already there, rendered at ip.mediolano.app/docs). Core carries **only thin pointers.**

---

## 3. Corrections (from legacy `developers`/`permissionless-setup`)

- Old GitHub org `mediolano-app` / `mediolano` → **`mediolano-os`**.
- **No hardcoded contract addresses** in core (app/deployment detail).
- **Do not assert** a published `@mediolano/sdk`, REST/OpenAPI API, or "Subgraphs" — unverified and
  Ethereum-ecosystem-flavored. Reference only the real contracts + repos. If a published SDK/API is
  later confirmed, link it then.
- Keep the affirmative Berne framing (consistent with the rest of the docs).

---

## 4. Artifacts & home

```
docs/guides/
  build-on-mediolano.md
```
Plus: a **Build** entry + an app pointer in `docs/README.md` (hub) and root `README.md`.

Legacy sources (review only; not copied into core): `mediolano-app/src/app/docs/{developers,
permissionless-setup}/`.

---

## 5. `guides/build-on-mediolano.md` — design

Accessible, layered, principle-level (no addresses, no asserted SDK). Sections:

1. **Build without asking** — Mediolano is a public, permissionless, zero-fee, immutable substrate;
   anyone can build on it, no gatekeeper.
2. **What you build on** — the immutable contracts (`mediolano-os/mediolano-contracts`); on-chain
   state is the source of truth; standard token interfaces + metadata make assets readable
   everywhere.
3. **Three ways to build** —
   - **Read & index** on-chain state (clients, explorers, indexers, analytics);
   - **Interact** with existing service contracts (the protocol's capabilities);
   - **Deploy** your own service contracts that compose with the protocol — "grow by adding
     services" ([06](../architecture/06-service-model.md)).
   All permissionless, non-custodial, zero-fee.
4. **AI agents are first-class** — same access on equal terms; machine-readable state and metadata
   ([07](../architecture/07-identity.md)).
5. **Resources** — links: `mediolano-os` (GitHub org), `mediolano-os/mediolano-contracts`, the
   [architecture](../README.md), the [glossary](../glossary.md). Note that tooling/SDKs are evolving
   and are not asserted here.
6. **Using the reference app** — thin pointer to <https://ip.mediolano.app>; note its usage and
   local-setup guides live with the app, not in the protocol core.

Links: [Protocol & Applications](../architecture/03-protocol-and-apps.md),
[Service Model](../architecture/06-service-model.md), [Identity](../architecture/07-identity.md).

---

## 6. Authoring rules

- Defer to the axioms; consistent with `00`–`09`.
- Docs gate per file (no `medialane`; no roadmap/timeline promises; present-reality allowed).
- No hardcoded addresses; no asserted SDK/API; correct org to `mediolano-os`.
- All inter-doc links resolve.

---

## 7. Out of scope

- The app-side guides (`dapp-guide`, `user-guide`, `permissionless-setup`) — not edited this slice.
- Contract-level reference / SDK docs — when contracts/SDK are tackled.
- Docs-site tooling; publishing the repo public.

---

## 8. Deferred / open

- Linking a real SDK/API once one is published.
- Relocating/refreshing the app-side guides in the app repo — a separate, app-repo effort.
- This completes the legacy-docs review/rebuild into `mediolano-core` (app guides intentionally
  remain app-side).
