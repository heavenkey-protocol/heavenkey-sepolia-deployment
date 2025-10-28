# 💠 Heavenkey – Ethereum Digital Continuity Protocol

## Overview

**Heavenkey** is a modular inheritance and recovery protocol built exclusively on Ethereum.  
It automates secure digital succession and ethical fund redistribution through privacy-preserving smart contracts.

> “Heavenkey ensures that your digital assets never die with you —  
> they continue to serve a purpose aligned with your will and values.”

Heavenkey introduces a **Proof-of-Activity** inheritance system based on the **Diamond Standard (EIP-2535)**.  
The protocol allows users to:

- Define heirs and fallback recipients in advance  
- Detect inactivity on-chain through automated “ping” signals  
- Trigger inheritance and fund redistribution without intermediaries  
- Protect privacy using encrypted heir data (IPFS + XMTP)  
- Ensure autonomy through gas reserves and automated execution  

Heavenkey combines **security, automation, and ethics** to prevent digital asset loss and create continuity within the Ethereum ecosystem.

---

## Network

- **Ethereum Sepolia Testnet** – main deployment for testing and validation  
- Contracts are deployed and verified privately under the **Heavenkey Source License (BSL)**  
- Contract addresses are intentionally partially redacted for security reasons  

### Deployed Contracts (Sepolia)

| Module | Address (partial) |
|---------|------------------|
| Diamond Core | `0x7A3...dF32` |
| PlanManagementFacet | `0x1B9...44E1` |
| InheritanceFacet | `0xA27...59FA` |

---

#**Diamond Standard (EIP-2535)** → modular and upgradable contract system  
Heavenkey is composed of independent facets sharing a single Diamond storage, ensuring scalability, security, and upgradeability.

| Facet | Role |
|-------|------|
| **DiamondLoupeFacet** | Introspection and interface discovery (EIP-2535 compliance) |
| **PlanManagementFacet** | Creation and configuration of inheritance plans |
| **PlanMonitorFacet** | Ping, inactivity detection, and automated plan activation |
| **InheritanceFacet** | Heir claim logic and fallback trigger |
| **GasManagerFacet** | Gas reserve management and automation safety |
| **ConfigFacet** | Global parameters, treasury and fallback settings |
| **FallbackFacet** | Ethical redistribution of unclaimed funds |
| **TreasuryFacet** | Protocol treasury management |
| **OwnershipFacet** | Access control and protocol ownership |
| **Diamond Core** | Central router for all facet selectors |

Each module operates autonomously but integrates seamlessly through shared Diamond storage.
---

## Technical Highlights

| Feature | Description |
|----------|-------------|
| 🕓 Proof-of-Activity | Detects user inactivity through scheduled pings |
| 🔐 Privacy Layer | Encrypted heir data on IPFS + XMTP |
| ♻️ Ethical Fallback | Redistributes dormant funds to public goods |
| ⚙️ Gas Reserve | Guarantees autonomous contract execution |
| 🧩 Modular Diamond | Clean, extensible, upgradable architecture |
| 🧾 Test Coverage | 96 % (84 successful test cases) |

More details can be found in `Heavenkey_Test_Report.md` and `SECURITY.md`.

---

## Roadmap

See `ROADMAP.md` for detailed milestones.

| Phase | Goal | Status |
|-------|------|--------|
| MVP | Diamond + Inheritance facets complete | ✅ |
| V1 | **Audit + Chainlink Integration + Frontend/Security improvements** | 🔜 |
| V2 | ERC-4337 wallet integration + multi-asset support | ⏳ |
| V3 | Heavenkey DAO & public governance | ⏳ |

Current Stage: **MVP (tested on Sepolia)**  
Next Milestone: **Independent audit + mainnet launch (Q2 2026)**

---

## Impact

Heavenkey prevents the permanent loss of dormant ETH and promotes **ethical redistribution**.  
It aligns with Ethereum’s principles of decentralization, transparency, and public good.

Full details are available in `ImpactStatement.md`.

---

## Documentation

| File | Description |
|------|-------------|
| `whitepaper_EN.pdf` | Technical & philosophical overview |
| `Heavenkey_ExecutiveSummary.pdf` | One-page summary for grants |
| `Heavenkey_GrantRequest.pdf` | EF Grant Application (Q4 2025) |
| `Heavenkey_Test_Report.md` | Test coverage & validation |
| `SECURITY.md` | Security principles & audit plan |
| `ROADMAP.md` | Development milestones |
| `ImpactStatement.md` | Social & ethical alignment |

---

## Demo

🎥 **Watch the MVP Demo** (`media/heavenkey-demo.mp4`)

The demo shows:
- creation of an inheritance plan  
- heir claim sequence  
- automatic fallback redistribution simulation on Sepolia  

> (The full smart-contract logic and front-end are kept private pending audit.)

---

## License

**Heavenkey Source License v1.0 (Business Source License)**

- The author retains full commercial usage rights.  
- Public availability of this repository does not grant permission for production use, deployment, or derivative works until the **Change Date – October 8 2029**.  
- After that date, Heavenkey automatically transitions to **AGPL-3.0**.

See `LICENSE_HEAVENKEY_BSL.txt` and `NOTICE_HEAVENKEY.txt` for complete legal terms.

---

## Compatibility

- 🟣 Ethereum Mainnet & Sepolia  
- 🧩 Fully EVM-compatible  
- ⚙️ ERC-4337-ready architecture

---

## Contact

**Francesco Ventura**  
Founder & Lead Architect – Heavenkey Protocol  

🌐 GitHub: [heavenkey-protocol](https://github.com/heavenkey-protocol)  
✉️ Email: [info@francescoventura.it](mailto:info@francescoventura.it)  



## 🧾 Authorship & Licensing Proofs

> The Heavenkey Ethical Fallback mechanism and related licensing materials  
> have been timestamped and permanently registered on the Ethereum Mainnet.  
> These documents serve as immutable proof of intellectual authorship and ethical intent.  
>  
> 🔒 All original proofs (hashes, transactions, declarations) remain archived off-chain  
> until completion of the independent security audit (V1 milestone).

---

**Heavenkey © 2025 — Built for Ethereum, guided by ethics.**
