# Security

> This is general information about Mediolano's security posture and risks — not financial advice.

---

Mediolano's security comes from its design: immutable, neutral, verifiable primitives that no one —
not even their authors — can quietly change.

## 1. Security posture

- **Immutable primitives.** The contracts have no admin, owner, or upgrade switch. There is no
  privileged key that can alter a record, redirect a transfer, or change the rules after the fact.
  The protocol evolves by redeploy, not by mutation.
- **Audited and verifiable.** Contracts are audited, and the whole stack is verifiable end to end —
  anyone can check the code and the on-chain state. There are no hidden backdoors.
- **Security through simplicity.** Clean, narrow contracts are easier to reason about and harder to
  break than sprawling, upgradeable systems.

→ Go deeper: [Principles](../architecture/01-principles.md).

## 2. Non-custodial by design

Mediolano **holds nothing and can freeze nothing.** You control your own assets and keys, and you
interact with the immutable contracts directly. Any risk is to **your own self-custodied assets** —
there is no pool of user funds held by Mediolano to be lost or seized, because Mediolano never
takes custody.

## 3. Inherent risks

Smart contracts and blockchains carry inherent risk. Despite audits and testing:

- bugs in a contract, a client, or the underlying network (Starknet, Ethereum, or any chain
  Mediolano runs on) could put your assets at risk;
- transactions are irreversible — a mistaken or malicious transaction you sign cannot be undone;
- you are responsible for the keys that control your assets.

Use caution, and understand what you are signing.

→ Go deeper: [Chain Sovereignty](../architecture/08-chain-sovereignty.md).

## 4. Good practices

- **Guard your keys.** Anyone with your keys controls your assets. Use reputable wallets and, where
  possible, hardware signers.
- **Verify before you sign.** Check contract addresses and metadata; read what a transaction does
  before approving it.
- **Mind what you publish.** On-chain records are public and permanent; do not commit anything you
  are not prepared to make permanent.

## 5. Responsible disclosure

Security reports are welcome and valued. A dedicated disclosure channel is being established
*(provisional — to be confirmed)*; in the meantime, please reach the team through the public
community channels. Please disclose responsibly and give maintainers time to respond before going
public.
