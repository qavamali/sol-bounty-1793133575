# RaptorX Research Challenge: Ask Better Questions. Find Better Alpha.

An institutional-grade on-chain intelligence and quantitative alpha-generation engine engineered for the RaptorX ecosystem. This repository implements an end-to-end framework that shifts on-chain research from reactive dashboards to proactive, hypothesis-driven alpha discovery on Solana and EVM/DeFi liquidity layers.

---

## 1. Executive Summary & Thesis

Traditional crypto research fails because analysts ask superficial questions:
- *“What is the top volume token today?”* (Trailing, noise-heavy, late).
- *“Which wallet made the highest PnL last week?”* (Survivorship bias, copy-trade honey-pots).

**RaptorX Core Paradigm: Ask Better Questions. Find Better Alpha.**
To find asymmetric alpha before the curve, research must interrogate structural micro-mechanisms:
1. **Flow Asymmetry & Toxic Flow:** Is high-volume DEX trading accompanied by aggressive inventory offloading across concentrated liquidity pools before major oracle updates?
2. **Cluster Graph Latency & Entity Attribution:** Are separate pseudonymous wallets funding through discrete splitters but exhibiting synchronized sub-second swap execution via shared Jito MEV bundles?
3. **Perpetual DEX Open Interest vs. Spot Absorption Divergence:** Where is Open Interest (OI) expanding aggressively alongside negative funding rates while spot order books absorb sell-side delta without price contraction?
4. **Liquidity Velocity & Real Yield Runaway:** Which protocols are experiencing sudden spikes in fee-to-TVL velocity driven by organic retail interactions rather than mercenary wash-trading incentives?

This project provides both the **Analytical Research Paper** and the **Production Quantitative Engine** (`raptorx-alpha-engine`) that formalizes, calculates, and surfaces these alphas in real time.

---

## 2. Research Methodologies & Heuristic Formulas

### 2.1 Entity Graph Clustering (Disjoint Set Union & Bundle Temporal Proximity)
To identify single-actor syndicates masking their size across multiple wallets:
- **Temporal Proximity Threshold:** $\Delta t \le 1.2\text{ seconds}$ (same slot / block).
- **Graph Co-occurrence Weight:**
  $$\mathcal{W}_{ij} = \sum_{k=1}^{N} \exp\left(-\frac{\Delta t_k}{\tau}\right) \cdot \mathbb{I}(\text{asset}_i = \text{asset}_j)$$
  Where $\tau$ is the slot decay parameter and $\mathbb{I}$ is the target asset identity indicator.

### 2.2 Informed Flow Metric (ToxFlow Score)
Measures the directional toxicity of order flow against Automated Market Makers (AMM) and Central Limit Order Books (CLOBs):
$$\text{ToxFlow}(t) = \frac{\sum_{i \in \text{Txs}} \Delta P_{t, t+k} \cdot V_i \cdot \text{Sign}(D_i)}{\sum_{i \in \text{Txs}} V_i}$$
Where:
- $\Delta P_{t, t+k}$ is the forward mark-price drift $k$ seconds post-fill.
- $V_i$ is nominal volume of trade $i$.
- $\text{Sign}(D_i) \in \{+1, -1\}$ denotes buyer or seller aggression.
- A persistently high positive $\text{ToxFlow}$ indicates informed insider/syndicate accumulation before external market repricing.

### 2.3 OI/Spot Absorption Divergence (Alpha Reversal Index - ARI)
Identifies predatory short-squeezes and smart money accumulation:
$$\text{ARI} = \frac{\Delta \text{OI}_{\text{perp}} \times (-f_{\text{rate}})}{\sigma_{\text{vol}}} \times \left(1 + \frac{\text{Net Spot Inflow}}{\text{DEX Depth}_{\pm 2\%}}\right)$$
When perpetual funding is deeply negative ($f_{\text{rate}} < 0$) while open interest skyrockets and spot liquidity absorbs the inventory without downward slippage, ARI breaches the critical alpha boundary ($\text{ARI} > 2.5$), generating high-conviction long signals.

---

## 3. System Architecture

```
                          ┌────────────────────────┐
                          │ Solana RPC / Helius /  │
                          │   Geyser Streaming     │
                          └───────────┬────────────┘
                                      │ (Real-time Block Engine)
                                      ▼
                      ┌────────────────────────────────┐
                      │  RaptorX Ingestion & Normalizer│
                      └───────────────┬────────────────┘
                                      │
            ┌─────────────────────────┼─────────────────────────┐
            ▼                         ▼                         ▼
   ┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐
   │ Wallet Cluster  │       │  Informed Flow  │       │ Perp/Spot Delta │
   │  Graph Engine   │       │ Microstructure  │       │   Divergence    │
   └────────┬────────┘       └────────┬────────┘       └────────┬────────┘
            │                         │                         │
            └─────────────────────────┼─────────────────────────┘
                                      ▼
                      ┌────────────────────────────────┐
                      │   Hypothesis Evaluation Core   │
                      │  - "Better Question" Filters   │
                      │  - Multi-factor Scoring Engine │
                      └───────────────┬────────────────┘
                                      ▼
                      ┌────────────────────────────────┐
                      │ Actionable Alpha Intelligence  │
                      │  - Terminal Dashboard          │
                      │  - Instant Webhook Alerts      │
                      │  - JSON Structured Research API│
                      └────────────────────────────────┘
```

---

## 4. Key Features

- **Sub-Slot Bundle De-anonymizer:** Detects covert syndicate accumulation masked across up to 50 distinct addresses executed via Solana MEV tip accounts.
- **Microstructure ToxFlow Scanner:** Calculates forward markout price drift to detect high-probability institutional front-running or early protocol thesis accumulation.
- **Cross-Venue Perp Funding Divergence:** Compares Drift/Zeta perp skew vs. Raydium/Orca/Phoenix spot order absorption.
- **Automated Research Report Generator:** Produces markdown/JSON executive intelligence briefs summarizing hypotheses, statistical evidence, and confidence intervals.
- **Production-Ready & Fully Typed:** Built with zero mock dependencies—includes a resilient synthetic backtester & real-time RPC adapter.

---

## 5. Getting Started & Installation

### Prerequisites
- Node.js >= 18.0.0
- npm or pnpm
- Solana RPC URL (Optional for live mainnet streaming; defaults to internal historical micro-replay generator)

### Setup
```bash
# Clone the repository
git clone https://github.com/superteam-earn/raptorx-research-challenge.git
cd raptorx-research-challenge

# Install dependencies
npm install

# Build TypeScript source
npm run build

# Run the RaptorX Alpha Discovery Engine
npm start
```

### Configuration (`.env`)
```env
PORT=3000
SOLANA_RPC_URL=https://api.mainnet-beta.solana.com
MIN_CONFIDENCE_THRESHOLD=0.75
ENABLE_ALERT_LOGGING=true
```

---

## 6. Verification and Sample Output

Running `npm start` executes the automated hypothesis pipeline across on-chain states and produces structured alpha discoveries:

```
[RAPTOR-X] Ingested 1,420 transactions across 12 token pools.
[CLUSTER] Identified covert entity syndicate: Cluster #Alpha-09 (4 addresses, 99.4% cross-bundle temporal correlation).
[TOXFLOW] Detected anomalous toxic buyer accumulation on token $SOLV-PERP (Score: +0.84, Drift: +4.2%).
[DIVERGENCE] ARI Alert: Negative funding (-0.082%/h) with spot absorption on Orca CLMM pool.
[DISCOVERY] Generated Research Thesis: "Syndicate Short Squeeze & Accumulation on $SOLV".
```