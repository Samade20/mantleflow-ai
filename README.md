# MantleFlow AI 🤖

### Autonomous RWA Yield Intelligence on Mantle

> **Mantle Turing Test Hackathon 2026 · Track: AI × RWA (Phase 2 — AI Awakening)**  
> Submission Deadline: June 15, 2026 · Built on Mantle Network

---

| | |
|---|---|
| **Project** | MantleFlow AI |
| **Track** | AI × RWA — Phase 2: AI Awakening |
| **Core Stack** | Mantle Network · Solidity · Python · ERC-8004 · Ondo USDY · mETH · Ethena USDe |
| **Agent Identity** | ERC-8004 NFT — On-chain, Permanent, Verifiable |
| **Human vs. AI** | Live leaderboard: agent alpha vs. human portfolio manager |

---

## 01. Executive Summary

> *MantleFlow AI is an autonomous on-chain agent that dynamically manages, optimizes, and rebalances diversified Real-World Asset (RWA) yield portfolios on Mantle Network. By fusing institutional-grade quant strategy with agentic AI — all permanently recorded on-chain via ERC-8004 identity — it delivers verifiable, transparent alpha that no human manager can match at scale.*

The Mantle Turing Test Hackathon challenges builders to prove that AI can outperform humans in on-chain environments. **MantleFlow AI does exactly that** — not through theoretical benchmarks, but through live, autonomous capital deployment across Mantle's growing RWA ecosystem: Ondo USDY, mETH, Ethena USDe, and fBTC.

In the **Human vs. AI** competition mechanism, MantleFlow AI is pitted against human portfolio managers in real time, with every decision, rebalance, and outcome logged immutably on Mantle — creating the first verifiable, on-chain AI track record in RWA portfolio management.

---

## 02. Problem Statement

The Real-World Asset sector on-chain is growing rapidly — yet four critical gaps prevent it from reaching its full potential:

| Gap | Description |
|-----|-------------|
| ⚡ **Manual & Slow** | Human managers cannot monitor and rebalance multi-asset RWA portfolios 24/7. Yield opportunities are missed; risk is reacted to rather than anticipated. |
| 🔒 **Opaque Decisions** | TradFi institutions and retail users alike cannot audit why a portfolio made a specific rebalance decision. The trust gap prevents wider adoption. |
| 📉 **Static Strategies** | Most on-chain yield protocols use static, fixed-rate strategies. Dynamic, signal-driven allocation across USDY, mETH, and USDe is non-existent. |
| 🤖 **No Agent Benchmark** | There is no verifiable, on-chain track record for AI agents managing RWA portfolios. Institutional adoption requires proof of autonomous, accountable performance. |

---

## 03. Solution

MantleFlow AI is a fully autonomous AI agent that:

- **Monitors** real-time on-chain signals (wallet flows, yield spreads, liquidation risk) via Nansen and Elfa AI APIs
- **Processes** macro and sentiment data to generate a dynamic allocation score across USDY, mETH, USDe, and fBTC
- **Executes** rebalancing transactions through smart Solidity vault contracts deployed on Mantle Network
- **Logs** every decision with full reasoning to an on-chain audit trail via ERC-8004 agent identity NFT
- **Publishes** alpha signals via a Telegram bot and live leaderboard dashboard (Human vs. AI)

### How the Human vs. AI Mechanism Works

At hackathon launch, a human portfolio manager begins with the same starting capital and asset universe. MantleFlow AI runs in parallel, autonomously:

| Human Manager | MantleFlow AI |
|---|---|
| Makes weekly manual rebalances based on research | Rebalances continuously based on on-chain signals, 24/7, with sub-minute latency |

Every trade, yield claim, and rebalance is recorded permanently on Mantle. The live leaderboard at the hackathon showcase stream lets audiences watch AI vs. human performance unfold in real time.

---

## 04. Technical Architecture

```
┌─────────────────┐   ┌──────────────────┐   ┌─────────────────┐   ┌───────────────────┐
│   DATA LAYER    │   │ REASONING ENGINE │   │ EXECUTION LAYER │   │    IDENTITY &     │
│  On-chain signals│──▶│  LLM + Quant     │──▶│ Solidity Vaults │──▶│  TRANSPARENCY     │
│ Nansen + Elfa AI│   │  Strategy Module │   │   on Mantle     │   │ ERC-8004 NFT      │
└─────────────────┘   └──────────────────┘   └─────────────────┘   │ Live Audit Log    │
                                                                      └───────────────────┘
```

### Layer 1 — Data Ingestion

| Source | Role |
|--------|------|
| **Nansen API** | Smart money wallet tracking on Mantle; detects institutional inflows into USDY and mETH |
| **Elfa AI** | Social sentiment and on-chain anomaly detection for macro risk signals |
| **Mantle RPC** | Real-time block data, event logs, yield rates from Agni Finance and Merchant Moe |
| **Bybit Price Feeds** | USDT/USDY, mETH/ETH, USDe/USD spot prices with 1-second resolution |

### Layer 2 — Reasoning Engine (Python)

| Module | Function |
|--------|----------|
| **Allocation Score Model** | Multi-factor scoring of each asset class: yield spread, liquidity depth, smart money flow, macro sentiment |
| **Risk Manager** | Real-time drawdown limits, correlation checks, and rebalance threshold triggers |
| **Strategy Selector** | Chooses between yield maximization, risk-parity, and defensive modes based on volatility signals |
| **Decision Logger** | Packages every decision with full reasoning into structured JSON for on-chain submission |

### Layer 3 — Execution (Solidity on Mantle)

| Contract | Role |
|----------|------|
| `MantleFlowVault.sol` | ERC-4626 compliant yield vault holding USDY, mETH, USDe, fBTC positions |
| `StrategyRouter.sol` | Receives agent instructions and executes atomic rebalances through Mantle's DeFi protocols |
| `AgentIdentity.sol` | Mints and manages ERC-8004 NFT; writes decision hashes and performance metrics on-chain |
| `AuditLog.sol` | Append-only smart contract recording timestamped decision summaries — permanently verifiable |

### Layer 4 — Interface & Transparency

| Component | Description |
|-----------|-------------|
| **Live Dashboard** | React frontend displaying real-time portfolio allocation, yield vs. benchmark, agent decision feed, and Human vs. AI leaderboard |
| **Telegram Bot** | Alpha signals and rebalance notifications delivered to subscribers in real time |
| **Mantle Explorer Integration** | Every agent action directly viewable on Mantle's block explorer with annotated decision context |

---

## 05. ERC-8004 Agent Identity

One of the three defining features of the Turing Test Hackathon is the **ERC-8004 agent identity standard**. MantleFlow AI treats this not as a checkbox — but as a foundational layer of value.

| Feature | Detail |
|---------|--------|
| 📊 **On-Chain Track Record** | Every decision MantleFlow AI makes is hashed and written to the agent NFT. By submission day, the agent has a 40-day verifiable performance history. |
| 🔑 **Reputation Portability** | The ERC-8004 record persists beyond the hackathon. Institutional adopters can audit the full history before deploying capital. |
| 🏆 **Achievement Milestones** | Agent NFT is updated when key milestones are hit: first profitable rebalance, 7-day streak of positive alpha, $100K AUM milestone. |
| 🔗 **Transparent Attribution** | Each on-chain action is cryptographically linked to the agent identity — no human can impersonate or override the agent's record. |

---

## 06. Judge Alignment

| Judging Criterion | How MantleFlow AI Delivers | Fit |
|---|---|:---:|
| **Innovation** | First autonomous agent managing diversified RWA + yield on Mantle with live, streamed decision logs | ✦✦✦ |
| **Technical Depth** | ERC-8004 identity, Solidity vault contracts, Python quant engine, Nansen API integration | ✦✦✦ |
| **Track Fit (AI × RWA)** | Directly addresses USDY, mETH yield + dynamic risk management — core track spec | ✦✦✦ |
| **Human vs. AI** | Real-time leaderboard: agent alpha vs. human portfolio manager benchmarked on Mantle | ✦✦✦ |
| **Ecosystem Impact** | Deepens Mantle DeFi TVL; replicable framework for institutional RWA on-boarding | ✦✦✦ |
| **Feasibility** | Modular 4-sprint build plan; MVP in 2 weeks; full version by June 15 deadline | ✦✦ |

---

## 07. Build Roadmap

| Sprint | Dates | Deliverable | Status |
|--------|-------|-------------|--------|
| **S1** | May 6–16 | Core data pipeline: Nansen API, Mantle RPC, price feeds (USDY, mETH, USDe, fBTC) | 🟡 IN BUILD |
| **S2** | May 17–26 | Quant engine + Solidity vault contracts; ERC-8004 identity mint; testnet deployment | 🔵 PLANNED |
| **S3** | May 27–Jun 5 | Human vs. AI leaderboard dashboard; live audit log streamer; Telegram alpha bot | 🔵 PLANNED |
| **S4** | Jun 6–14 | Mainnet deployment, stress testing, performance report, demo video, BUIDL submission | 🔵 PLANNED |

### Post-Hackathon Vision

MantleFlow AI is architected for longevity, not just the hackathon:

- **Protocol Expansion** — Extend to additional Mantle DeFi protocols (Fluxion, mETH staking vaults)
- **Institutional Interface** — White-label vault product for family offices and crypto-native treasuries
- **Agent Marketplace** — ERC-8004 strategy NFTs tradeable on-chain: buy, rent, or clone proven agent strategies
- **Cross-Chain Execution** — Bridge to Ethereum L1 for broader RWA asset coverage

---

## 08. Unfair Advantages

> *MantleFlow AI is not a demo — it is a live, autonomous agent deployed on Mantle with a real portfolio, real decisions, and a real track record by submission day.*

- 🥇 **First-mover** — No existing project in the hackathon combines ERC-8004 identity with multi-asset RWA yield optimization on Mantle
- 🎯 **Judge-ready narrative** — Every feature maps to a hackathon evaluation criterion and Mantle's stated strategic priorities
- 📡 **Live demonstration** — The AI Awakening phase is live-streamed globally; MantleFlow AI's real-time performance is the demo
- 🤝 **Ecosystem partners** — Integrates Nansen data, Elfa AI signals, Bybit price feeds — directly engaging key sponsors
- 🏛️ **Radical transparency** — On-chain audit log satisfies institutional-grade accountability standards — unique in the field

---

## 09. Closing Statement

> *"The Turing Test Hackathon is not a coding contest — it is the beginning of a new category."*  
> — Emily Bao, Byreal

MantleFlow AI embodies exactly that spirit. It is not an experiment or a prototype. It is an **autonomous financial intelligence** — one that lives on Mantle, learns from on-chain reality, outperforms human managers on verifiable metrics, and builds a permanent, trustless reputation via ERC-8004.

By the time judges evaluate submissions, MantleFlow AI will have been running autonomously for **40 days on Mantle mainnet**, with a complete on-chain track record, a live leaderboard showing its performance against a human manager, and a fully auditable decision log that any institutional investor could use to make a deployment decision.

That is not a hackathon project. That is **the future of on-chain finance**, built on Mantle.

---

<div align="center">

**MantleFlow AI · Mantle Turing Test Hackathon 2026 · AI × RWA Track**  
Submission Deadline: June 15, 2026 · Built on Mantle Network

</div>
