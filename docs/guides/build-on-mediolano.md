# Build on Mediolano

*How to build on Mediolano — a public, permissionless substrate for programmable IP. Plain idea
first, then the substance, then links for depth.*

---

Mediolano is public infrastructure. **Anyone can build on it without asking** — no gatekeeper, no
allowlist, no fee at the protocol layer, and nothing you build can be shut off by a central party.
You build on a set of clean, immutable smart contracts; what you make with them is yours.

## What you build on

- **Immutable contracts.** The protocol is a set of immutable Cairo contracts —
  [`mediolano-os/mediolano-contracts`](https://github.com/mediolano-os/mediolano-contracts) — with
  no admin, owner, or upgrade switch. What you build against will not change under you.
- **On-chain truth.** The chain is the source of truth; indexers, apps, and agents present it but
  never authorize it ([Protocol & Applications](../architecture/03-protocol-and-apps.md)).
- **Standard interfaces.** Assets use standard token interfaces and metadata, so anything you build
  interoperates with wallets, marketplaces, and other dapps out of the box.

## Three ways to build

**1. Read and index.** The whole protocol state is public. Build clients, explorers, indexers,
dashboards, or analytics on top of on-chain events — no permission required.

**2. Interact.** Call the protocol's existing service contracts directly to tokenize, license, and
compose IP. Your app, script, or agent talks to the contracts; Mediolano custodies nothing.

**3. Deploy your own services.** The substrate **grows by adding services, not editing them**. Deploy
your own immutable contracts that compose with the protocol and register the capabilities they offer
([Service Model](../architecture/06-service-model.md)). New capability arrives as a *new* service —
nothing already deployed changes.

All three are permissionless, non-custodial, and zero-fee at the protocol layer.

## AI agents are first-class

Agents build and act on the same terms as humans — there are no human-only paths and no anti-agent
gates. On-chain state and metadata are machine-readable, so an agent can read provenance, verify
license terms, and transact directly ([Identity](../architecture/07-identity.md)).

## Resources

- **GitHub:** the [`mediolano-os`](https://github.com/mediolano-os) organization, and the contracts
  at [`mediolano-os/mediolano-contracts`](https://github.com/mediolano-os/mediolano-contracts).
- **Architecture:** the [full foundation](../README.md) and the [glossary](../glossary.md).

Higher-level tooling and SDKs are evolving; this guide stays at the level of the contracts and
repositories themselves.

## Using the reference app

To *use* Mediolano rather than build on it, the IP Creator is live at <https://ip.mediolano.app>.
Its usage and local-setup guides live with the app — this protocol core stays focused on what you
build on, not on any single application.

---

→ Related: [Protocol & Applications](../architecture/03-protocol-and-apps.md) ·
[Service Model](../architecture/06-service-model.md) · [Identity](../architecture/07-identity.md).
