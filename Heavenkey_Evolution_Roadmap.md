Heavenkey — Evolution Roadmap
🛠️ MVP — The Foundation: Architecture Validation (Completed)
Mission

Prove beyond doubt the core thesis of Heavenkey:

👉 It is possible to build a decentralized, non-custodial, privacy-first, automatic, and ethical digital inheritance system on Ethereum.

The MVP demonstrates, with a working implementation (local + Sepolia), that Heavenkey’s succession logic is secure, reliable, and ready to be hardened and audited.

Design Philosophy

Security first → OpenZeppelin standards, CEI pattern, minimized attack surface, modular Diamond architecture.

Non-custodial by definition → no key custody; funds are always governed by on-chain logic.

Privacy by design → heirs remain off-chain and encrypted; no identity appears on-chain until reveal.

Ethical outcome → if no heir claims, funds are routed to an Ethical Legacy Fallback (chosen by the user) + the protocol treasury.

Implemented Features (full lifecycle)

Plan Creation → createPlan() deploys plan on-chain, saves IPFS digest (AES-GCM encrypted per-heir payload), sets commits, defines Ethical Legacy Fallback, deposits ETH (min. 0.05 ETH on testnet, 2.5% fee, 0.01 ETH gas reserve).

Active Maintenance → ping() resets inactivity timer, keeps plan ACTIVE.

Automatic Succession → after timeout → plan moves to INACTIVE, sequential heir windows open (heir0 → heir1 …). Commits frozen at start.

Claim (commit–reveal) → claimInheritance(owner, heir, salt) checks commitment with domain separation, accepts only from active heir wallet, executes payout, closes plan.

Ethical Legacy Fallback → if all heirs fail, funds go to the user-chosen ethical recipient + treasury.

Commit formula:

commit[i] = keccak256(
  abi.encodePacked(
    DOMAIN,           // keccak256("HeavenkeyHeirCommit:v1")
    block.chainid,
    address(this),    // diamond
    owner,
    i,                // index
    heir,             // heir address
    salt              // claim code (bytes32)
  )
);

Architecture & Stack

Smart Contracts: Solidity ≥0.8.20, Diamond EIP-2535, shared AppStorage.

PlanManagement → plan lifecycle, IPFS digest, setHeirCommits.

PlanMonitor → ping(), inactivity, rotation, freeze commits.

Inheritance → commit–reveal, claim, payout.

Fallback → manages Ethical Legacy Fallback routing.

Treasury → fees & accounting.

Config → global parameters.

GasManager → gas reserve.

Off-chain (privacy-first): per-heir payloads encrypted with AES-GCM → IPFS; on-chain only digest + commits. Salt sent via XMTP E2EE (or OTP fallback) automatically when the heir’s window opens, even if the heir is not connected to the dApp.

Automation: Node.js keeper (local). Roadmap: migrate to Chainlink Automation (decentralized, observable, reliable).

Dev & Frontend: Hardhat test suite + scripts (resetLocalEnv, exportSalts, keeperAuto); React + ethers v6 dApp, UI with countdowns, Claim modal (paste code or auto-fill via XMTP), clear active/succession/fallback states.

🧪 MVP Validation

Concept → Automatic succession with native privacy + commit–reveal is feasible and robust.

Architecture → Diamond modular design ensures separation of concerns, auditability, and upgrade path.

Operations → End-to-end flow validated (local + Sepolia), sequential heir windows with frozen commits, multi-owner testing with salt exporter, coherent claims, Ethical Legacy Fallback tested.

⚠️ MVP Limitations

Centralized keeper (local) → V1: Chainlink Automation.

No external audit → V1: Tier-1 Audit + Immunefi bug bounty.

Secret management (.env) → V1: Vault, key rotation, least privilege.

Incomplete cryptographic binding → V1: AES-GCM + AAD bound to plan/window.

UX & mobile limited → V1: professional UI/UX, mobile support, granular error handling.

ETH-only → V2: ERC-20 (USDT), NFT visibility.

Non-gasless claim → V2: ERC-4337 + Paymaster, EIP-1271 signatures.

Testnet accelerated parameters: ping=180s, inactivity=240s, heirWindow=120s, minDeposit=0.05 ETH.

🛡️ V1 — The Fortress: Security, Decentralization & Mainnet Launch
Mission

Transform the validated architecture into a fortress: eliminate centralization, pass professional audits, and launch on mainnet under controlled conditions.

Key Objectives

Decentralized automation → replace local keeper with Chainlink Automation on PlanMonitorFacet.

Privacy hardening → AES-GCM + AAD (plan/window binding), stable commit–reveal with EIP-712/1271, XMTP/OTP delivery with rate-limits.

Mainnet security → Tier-1 Audit across all facets, Immunefi bug bounty, remediation.

Economics → ConfigFacet: 2.5% fee, $125/year subscription, gas reserve, deposit caps.

Heirs → up to 4 heirs supported on mainnet (MVP: 2 heirs on testnet).

V1 Roadmap

Chainlink Automation integration on testnet + telemetry.

Code freeze → full audit + bug bounty.

Gated mainnet launch (deposit caps) → progressive public rollout.

🌐 V2 — The Smart Vault: Multi-Asset & Invisible UX
Mission

Evolve from fortress to smart vault: support multiple assets and frictionless user experience.

Key Features

Multi-asset support → ERC-20 (USDT) and NFTs (ERC-721).

Legacy Statement → message/document (IPFS/Arweave hash) signed via EIP-712/1271, delivered with assets.

Smart Wallets (ERC-4337) → gasless claim via Paymaster, EIP-1271 signatures, simplified heir UX.

V2 Roadmap

Development of new multi-asset facets.

Public testnet + modular audits.

Progressive mainnet release via diamondCut.

🏛️ V3 — Public Infrastructure: Standard & Governance
Mission

Turn Heavenkey into a public, ethical, and perpetual infrastructure: an on-chain inheritance standard governed by the community.

Pillars

Standardization via Account Abstraction (ERC-4337) → inheritance plan becomes a native policy module of Smart Accounts.

Guardian Guild DAO → governance token $HKEY, treasury, parameters, roadmap.

Optional Yield (opt-in) → ERC-4626 adapters for allowlisted protocols (Aave, Lido, Compound), with circuit breakers & pause, activated only with DAO approval + audits.

🏁 Conclusion

Heavenkey evolves in phases:

MVP (Foundation) → architecture validated, commit–reveal, Ethical Legacy Fallback proven.

V1 (Fortress) → security, decentralized automation, audit, controlled mainnet launch.

V2 (Vault) → multi-asset, Legacy Statement, gasless claim.

V3 (Infrastructure) → global ethical inheritance standard, DAO-governed, optional yield.

👉 The constant foundation: Ethical Legacy Fallback → ensuring unclaimed assets are never lost, but redirected into social good.

Heavenkey stands as a living proof that ethics and automation can coexist on-chain.