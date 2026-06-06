# Frequently Asked Questions

Common questions about Mediolano — the public-goods substrate for tokenizing, protecting, and
licensing intellectual property. For depth, follow the links at the end.

---

### What is Mediolano?

Mediolano is a public good for turning intellectual property into permanent, verifiable, and freely
usable records of authorship and ownership. It is neutral infrastructure: applications,
marketplaces, and agents build on top of it, and it answers to the
[Integrity Web Axioms](architecture/00-axioms.md).

### What can I tokenize?

A broad range of works — visual art, music and audio, writing and publications, video, software,
patents and inventions, research, posts, and real-world assets. If it can be authored, it can be
tokenized, protected, and licensed.

### Does it cost anything?

The protocol is **zero-fee**: the tokenization and protection primitives take no cut. Using a
particular application or paying a blockchain's network costs are separate matters, decided at the
app and chain layer — never by the substrate.

### Can I edit my IP after minting?

No — and that is the point. Records are **immutable**: authorship, ownership, and provenance cannot
be silently changed after the fact. That permanence is what makes the proof trustworthy.

### Who owns my IP?

You do. Mediolano is **non-custodial** — it never holds or restricts your assets. The contracts are
permissionless and you act directly through them.

### How is my authorship protected?

Through durable, independently verifiable records: ownership and provenance on-chain, content
committed in tamper-proof content-addressed metadata. Mediolano is built to align with the
[Berne Convention](https://en.wikipedia.org/wiki/Berne_Convention), under which authorship is
recognized across 180+ countries. See [how Mediolano protects IP](concepts/ip-protection.md).

### Can I choose a license?

Yes. Licensing is programmable and Creative-Commons-compatible, and **the creator chooses** the
terms — no protocol-wide default is imposed. See
[programmable licensing](concepts/programmable-licensing.md).

### Does my asset work on other wallets and marketplaces?

Yes. Assets use standard token interfaces and a standard metadata envelope, so they are readable by
third-party wallets, marketplaces, indexers, and agents — not just by Mediolano-specific tools.

### Can AI agents use Mediolano?

Yes — as first-class participants on equal terms with humans. There are no human-only flows and no
anti-agent gates; an identity is defined by what it can prove and sign, not by the kind of mind
behind it.

### What chains does it run on?

Mediolano is powered on Starknet and is designed to be **owned by no chain**: chains are peers, and
your identity and work are built to survive the loss of any single one. See
[Chain Sovereignty](architecture/08-chain-sovereignty.md).

### Are the contracts immutable and audited?

The primitives are **immutable by design** — no admin, no owner, no upgrade switch. They evolve by
redeploy, not by mutation. Audits are conducted and published openly.

### Is it open source?

Yes. Mediolano is neutral, forkable public infrastructure — anyone can read it, index it, fork it,
or build a competing client. There are no private interfaces.

---

**Go deeper:** [Litepaper](litepaper.md) · [Architecture](README.md) · [Glossary](glossary.md).
