Heavenkey – SECURITY.md

Last updated: 8 September 2025
Scope: Heavenkey MVP on Ethereum Sepolia (ETH-only, up to 4 heirs)

This document describes the MVP’s security posture, known limitations, and the hardening plan prior to Mainnet launch.

🔐 Security Principles

Non-custodial by design
Heavenkey never controls private keys. Funds are governed only by on-chain logic; they move either by the owner (while active) or the eligible heir during their window.

Transparent, modular contracts
Diamond (EIP-2535) architecture with specialized facets, shared AppStorage, and clear separation of concerns. Code is publicly reviewable.

Minimization of sensitive on-chain data
Heirs are not stored in clear on-chain. We keep commitments (hashes) and a bytes32 digest pointing to the encrypted IPFS blob.

No centralized database
No proprietary datastore for sensitive data. Per-heir payloads live on IPFS (encrypted); operational secrets are off-chain. In V1, secrets migrate to a vault with key rotation.

Protocol survivability
Even without a frontend or the team, contracts remain operable: ping, state transitions, claim, and fallback are all on-chain.

🧪 MVP Disclaimer (Sepolia)

Testnet only: use test ETH exclusively.

Parameters and code may change before Mainnet.

The MVP includes development-oriented simplifications, not meant for production.

🧱 Architecture & Data Flow (overview)

On-chain (Diamond facets)

Plan state machine: ACTIVE → inactivity → sequential heir windows → fallback.

Commit–reveal with domain separation and commitment freeze at succession start.

Commitment: keccak256(DOMAIN, chainId, diamond, owner, index, heir, salt)

Claims succeed only in the active window and only from msg.sender == heir.

Off-chain storage

One encrypted blob per plan on IPFS holds per-heir metadata. On-chain we store its bytes32 digest; IPFS resolution happens off-chain.

Notifications

The active heir receives the claim code (the salt, bytes32) via XMTP (E2EE) or—fallback—OTP with rate-limit and expiry.

Automation (MVP)

A local Node.js keeper monitors plans and triggers rotations/fallback. It exposes lightweight state signals to the UI.

🧠 Threat Model (summary)

Replay / cross-plan / cross-chain

Mitigation: domain separation in the commitment (DOMAIN, chainId, diamond, owner, index, heir, salt).

Front-running of claims

Mitigation: commit–reveal, msg.sender == heir, secret salt, commitment freeze once succession starts.

Reentrancy & CEI

Mitigation: strict Checks–Effects–Interactions, pull-style payouts where applicable, OpenZeppelin primitives.

Griefing / timing DoS

Mitigation: hard time windows, gas reserve for automated ops, clear facet separation.

Frontend/backend loss

Mitigation: all critical operations are on-chain; UIs are replaceable; heirs can interact directly with contracts.

⚠️ MVP Risks & Limitations

No formal external audit (yet)
Code has not been reviewed by third-party security auditors.

Centralized keeper (local)
Automation relies on a single Node.js process with .env secrets → potential SPOF.

Unsigned UI signal
Development JSON/artefacts used by the UI are not cryptographically authenticated.

Encryption: contextual binding in progress
Per-heir payloads use AES-GCM; AAD binding to plan/window is being hardened for V1.

Operational secret management
Keys and credentials live in .env during MVP.

🔧 Planned Security Improvements (V1+)

Chainlink Automation
Replace the local keeper with decentralized execution, retries, gas management, and observability.

AEAD + KDF & AAD binding
AES-256-GCM (or XChaCha20-Poly1305) with keys derived via scrypt/Argon2, per-blob nonce, AAD bound to plan/window, versioned envelope.

Commit–reveal & signatures (AA-ready)
Harden EIP-712/1271 paths for smart wallets (ERC-4337) and Paymaster compatibility (gasless claim in V2).

Signed UI signal
Replace temporary artefacts with signed and verifiable payloads (API/CDN).

Secret Management
Move to a vault (rotation, least privilege, audit trail), with access policies and controlled break-glass.

Formal audit + Bug bounty
Tier-1 audit across all facets & interactions; public Immunefi bounty.

Automated analysis
Integrate Slither (static), Echidna (fuzz/property), coverage monitoring, and differential testing.

Circuit Breaker (optional)
Targeted pauses on non-critical functions (never blocking user funds) to contain anomalies.

DAO-governed parameters
Progressively hand fee/fallback/treasury controls to the Guardian Guild DAO.

📬 Responsible Disclosure

Email: (temporarily: info@francescoventura.it)

PGP key: available on request

Bug bounty: details will be published after the audit and before Mainnet launch

📅 Changelog

28 October 2025

Synced with current MVP: on-chain commit–reveal with domain separation and commit freeze.

Clarified AES-GCM usage and V1 AAD plan.

Expanded Threat Model and Chainlink migration plan.


Clarified use of encrypted off-chain artefacts.

Added AEAD/KDF plan.

Documented on-chain claim authorization.

Highlighted keeper/UI limits and replacement with Chainlink + signed signal.

© Heavenkey Protocol 2025 — All rights reserved.

