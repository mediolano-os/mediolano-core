# Mediolano Litepaper

*An accessible overview of Mediolano — public-goods tokenization for the Integrity Web. Written
for everyone: read the first line of each section for the plain idea, keep reading for substance,
and follow the links to go as deep as you like.*

---

## 1. What Mediolano is

**Mediolano is a public good for turning intellectual property into permanent, verifiable, and
freely usable records of authorship and ownership.**

Anyone can use it to tokenize a work and create an on-chain record that proves who made it, when,
and under what terms. That record is immutable, costs nothing at the protocol layer, and belongs
to its creator — not to any company. Mediolano is the neutral foundation; applications,
marketplaces, indexers, and AI agents build on top of it.

The works it serves are deliberately broad: visual art, music and audio, writing and
publications, video, software, patents and inventions, research, posts, real-world assets, and
more. If it can be authored, it can be tokenized, protected, and licensed through Mediolano.

## 2. The problem

**Intellectual property today is fragile, gatekept, platform-locked, and trapped behind borders.**

Proof of authorship usually lives in a company's database — which can change its terms, lose your
records, go out of business, or lock you out. Rights are enforced by whoever owns the platform,
and your work is often only as portable as that platform allows: leave, and your provenance,
history, and audience may not come with you. Across jurisdictions, recognition is uneven and slow,
and formal registration is costly. Creators carry the risk while the infrastructure that should
serve them is owned by someone else — and monetized at their expense.

A durable creative economy needs the opposite: a foundation no single company controls, where a
record of authorship outlives any app, and where the rules cannot be rewritten after the fact.

## 3. The idea

**Tokenize intellectual property as a public good: durable, verifiable authorship that no single
company, app, or country can take away.**

Mediolano records authorship and ownership on-chain and in immutable, content-addressed metadata,
so the proof is permanent and checkable by anyone, forever. The protocol charges no fees and asks
no permission. It is part of the **Integrity Web** — a vision in which trust comes from
cryptographic proof rather than from authorities, and in which the infrastructure everyone depends
on is a shared commons rather than someone's private property. Every design choice in Mediolano
answers to the [Integrity Web Axioms](architecture/00-axioms.md).

## 4. How it works

**You mint a record of your work; the proof lives on-chain and in permanent metadata; the rights
travel with it.**

- **Immutable authorship records.** When a work is tokenized, its authorship, ownership, and
  provenance are written on-chain, where they cannot be silently altered. What is proven stays
  true.
- **Content-addressed metadata.** The work's details and license live in content-addressed storage
  (IPFS / Arweave), where the reference is itself the integrity check — the pointer resolves to
  exactly what was committed, or not at all.
- **Programmable licensing.** Usage terms are encoded in standard, widely-readable metadata that
  travels with the asset, so wallets, marketplaces, indexers, and agents all understand it. Terms
  are declared by default and enforced selectively, only where a specific service requires it.
- **Protocol, not app.** The chain is the source of truth. Apps and indexers present and organize
  it; they never *authorize* it, and the protocol keeps working even if any single one of them
  disappears.

→ Go deeper: [Core Model](architecture/02-core-model.md) ·
[Protocol & Applications](architecture/03-protocol-and-apps.md) ·
[Licensing & Authorship](architecture/05-licensing-and-authorship.md).

## 5. Built to grow: the service model

**Mediolano grows by adding new capabilities as services — without ever changing what already
exists.**

Beyond minting and licensing, Mediolano offers (and can keep adding) modular **services** for the
ways IP actually gets used: access and gated content, subscriptions and clubs, revenue sharing and
royalty splits, escrow and assignment, drops and airdrops, collections and editions, and
marketplace flows. Each service is a self-contained module that anyone can discover and build on.
New capability arrives by *adding* a service, never by editing an existing one — so a record made
today behaves the same way tomorrow.

→ Go deeper: [Service Model](architecture/06-service-model.md).

## 6. Why it's a public good

**The protocol is free, neutral, immutable, and open — infrastructure that belongs to everyone.**

- **Zero-fee.** The tokenization and protection primitives take no cut. A commons cannot meter the
  people it belongs to. Applications may build their own economic models *around* the protocol; the
  protocol itself stays free.
- **Neutral & immutable.** The primitives have no admin, owner, or upgrade switch. No one can
  change the rules under a record already made.
- **Open & forkable.** Anyone can read it, index it, fork it, or build a competing client. There
  are no private interfaces and no privileged clients.

These are the cypherpunk values often summarized as **CROPS** — Censorship-resistance,
Open-source, Privacy, Security — with *longevity over breadth* as the guiding instinct. Stewardship
of the commons is handled without extraction: there is nothing to meter and no treasury to skim.

→ Go deeper: [Principles](architecture/01-principles.md) ·
[Stewardship](architecture/09-stewardship.md).

## 7. For everyone, every intelligence

**Mediolano protects creators across borders, and treats humans and AI as equal participants.**

It is built to align with the [Berne Convention](https://en.wikipedia.org/wiki/Berne_Convention)
for the Protection of Literary and Artistic Works — the treaty under which authorship is
recognized across more than 180 countries (and, via TRIPS, most WTO members). Berne's core ideas
fit the protocol naturally: protection is automatic the moment a work is fixed, no registration is
required, and rights are recognized across member states independently of the country of origin.
Tokenizing on Mediolano creates a Berne-compliant, worldwide-recognized record of authorship and
ownership — a timestamped proof and licensing instrument that does, permissionlessly and at zero
protocol cost, what notarial and copyright-registration services charge for.

And it makes no distinction between forms of intelligence: humans, AI agents, organizations, and
future intelligences participate on the same terms. There are no human-only flows and no
anti-agent gates — an identity is defined by what it can prove and sign, not by the kind of mind
behind it. As culture is increasingly created with and by machines, the commons that records it
must belong to all of them.

→ Go deeper: [Licensing & Authorship](architecture/05-licensing-and-authorship.md) ·
[Identity](architecture/07-identity.md).

## 8. Owned by no chain

**Your identity and your work are anchored to proof, not trapped on any single chain.**

Mediolano treats verifiable trust as a *role, not a place*. No chain is its permanent home; chains
are peers. Identity and the record of who made what are designed to be portable and re-anchorable,
so they survive the loss of any single chain — and you always keep a way to move your assets and
identity out. The same zero-knowledge techniques that make claims verifiable also protect privacy:
you can prove something is true without revealing the data behind it.

→ Go deeper: [Chain Sovereignty](architecture/08-chain-sovereignty.md).

## 9. How to take part

- **Use it.** Tokenize and manage IP with the Mediolano IP Creator: <https://ip.mediolano.app>.
- **Build on it.** Mediolano is public infrastructure — index it, render it, or build your own
  client. The protocol and its documentation are open.
- **Steward it.** Join the community and help keep the commons neutral and durable:
  <https://t.me/integrityweb>.

## 10. Go deeper

- **[The Integrity Web Axioms](architecture/00-axioms.md)** — the governing authority.
- **[Architecture](README.md)** — the full foundation, from principles to chain sovereignty.
- **[Glossary](glossary.md)** — canonical terms.
