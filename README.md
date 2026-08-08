# ShadowStamp — Private Proof of Ownership

**Prove ownership. Reveal nothing.**

ShadowStamp is a privacy-first decentralized application built on the **Midnight Network** that lets users prove the ownership and existence of sensitive digital content — ideas, business plans, research, documents, code, artwork, AI prompts, and other intellectual property — **without ever revealing the original content**.

Instead of putting sensitive information publicly on-chain, ShadowStamp hashes content locally in the browser and records only a cryptographic commitment on Midnight. The original content never leaves the user's device.

---

## Live Deployment

- **Network:** Midnight Preview Testnet
- **Deployed Contract Address:** `e2922a8ca67d31baf5e2521b95c52ee6e16f87f967e0edf36f2c7f0dbde687f4`
- **Wallet Integration:** 1AM Wallet

---

## Features

- **Private proof creation** — content is hashed (SHA-256) and committed locally; only the commitment is submitted on-chain
- **1AM Wallet integration** — connect wallet to become the verifiable owner of a proof
- **On-chain verification** — anyone can verify a proof exists without seeing the original content
- **Optional reveal** — owners can choose to reveal their proof later
- **Proof dashboard** — searchable, filterable history of all stamped proofs with status tracking (generated → submitted → confirmed)
- **QR-based verification** — each proof generates a scannable QR code for portable verification
- **Downloadable certificates** — PNG proof-of-ownership certificates generated client-side
- **Categories** — organize proofs by type (general, code, research, artwork, etc.)

---

## Tech Stack

- **Frontend:** React + TypeScript + Vite
- **Smart Contract:** Compact language (Midnight's ZK smart contract language)
- **Blockchain:** Midnight Network (Preview testnet)
- **Wallet:** 1AM Wallet (`dapp-connector-api`)
- **QR Codes:** `qrcode.react`
- **Certificates:** HTML Canvas → PNG export

---

## Architecture

Content (text/file)
↓
Local SHA-256 hash + commitment (browser only — nothing leaves device)
↓
Compact smart contract (submitProof) — deployed on Midnight Preview
↓
On-chain: commitmentByHash map stores {hash, commitment, timestamp}
↓
Anyone can call verifyProof(hash) to confirm existence — without ever
seeing the original content.


---

## Getting Started

```bash
npm install
echo "VITE_1AM_NETWORK=preview" > .env
npm run compact
npm run dev
```

Then connect **1AM Wallet** (Preview network, testnet funded) and click **Stamp proof**.

---

## Engineering Notes

Getting a real Compact contract talking to a browser wallet involved resolving deep dependency-version conflicts inside Midnight's own SDK — duplicate WASM runtime instances caused `instanceof` identity mismatches (`_StateValue`) at the contract-submission boundary. Resolved by unifying package versions via `overrides` and Vite's `resolve.dedupe`.

---

## Status

| Component | Status |
|---|---|
| Compact contract (compile) | Complete |
| Frontend build & typecheck | Passing |
| Wallet integration (1AM) | Working |
| On-chain deployment | Live on Preview testnet |
| Proof creation & submission | Working |
| Verification / reveal | Implemented |
| QR + certificate generation | Implemented |

---

## Privacy Guarantee

At no point does the original content, file, or plaintext leave the user's device. Only a cryptographic hash and commitment are ever transmitted or stored on-chain.
