# Arc Ecosystem — Product Portfolio

Products we are building and proposing on **Arc**, Circle's stablecoin-native L1 (USDC as native gas; mainnet beta targeting summer 2026). Each one attacks a specific weakness in Arc or amplifies a strength.

- **[Active Portfolio](#active-portfolio-in-flight)** — what we're building now, described in full below.
- **[Full catalog →](CATALOG.md)** — the complete proposed slate, grouped by domain.
- **Scoring** — `Arc_Ecosystem_Product_Opportunities_Ranked.xlsx` scores every entry on first-mover, revenue, grant-fit, Arc-fit, and moat.

---

## At a Glance

| Domain | Ideas | What it targets |
|---|--:|---|
| [Confidential Finance](CATALOG.md#confidential-finance) | 6 | Privacy tooling (#5) |
| [Agentic Infrastructure](CATALOG.md#agentic-infrastructure) | 16 | Agentic adoption (#6) |
| [RWA and Compliance](CATALOG.md#rwa-and-compliance) | 15 | RWA & compliance (#8) |
| [FX and DeFi](CATALOG.md#fx-and-defi) | 21 | Permissionless FX & liquidity (#4) |
| [Payments and Activation](CATALOG.md#payments-and-activation) | 20 | Real on-chain activity (#1, #3) |
| [Trust and Verifiability](CATALOG.md#trust-and-verifiability) | 6 | Consortium-chain trust (#2) |
| [Fiat-to-Crypto Boundary](CATALOG.md#fiat-to-crypto-boundary) | 7 | Fiat-to-crypto ramps (#3) |
| [Data and Analytics](CATALOG.md#data-and-analytics) | 3 | Payments-native intelligence (#1, #8) |
| [Stablecoin Issuance](CATALOG.md#stablecoin-issuance) | 3 | New issuers & currencies (#3, #1) |
| [Cross-chain Infrastructure](CATALOG.md#cross-chain-infrastructure) | 3 | Settlement-hub orchestration (#3) |
| [Wallets and UX](CATALOG.md#wallets-and-ux) | 6 | Wallet & UX layer (#3) |
| [Developer Experience](CATALOG.md#developer-experience) | 7 | Developer tooling (#3) |
| [Governance and Token](CATALOG.md#governance-and-token) | 6 | Token, governance, accounting (#7) |
| [Trade and Vertical](CATALOG.md#trade-and-vertical) | 5 | Vertical settlement & financing (#1, #8) |
| [Consumer and Emerging-Market Apps](CATALOG.md#consumer-and-emerging-market-apps) | 4 | Demand-side / emerging-market (#1, #3) |

---

## Active Portfolio (In Flight)

The products already under construction — a connective-tissue payments stack plus standalone products. UPay dogfoods Relay; Tideline and ArcNS have live deployments.

### The Relay Cluster

A composable, non-custodial payments stack on top of Circle's Stablecoin Kit, filling the gaps Circle's own SDKs leave open. *(The `@usdkit/*` scope is retired — it collides with `@circle-fin/usdckit` — and a fresh scope is being chosen.)*

**Gateway SDK** — *Foundation.* A typed Circle Gateway SDK — deposit, withdraw, unified-balance, burn-intent — with bounded retries and a discriminated-union error model. Everything else in the cluster builds on it.

**Relay** — *Spine.* A durable, non-custodial **PaymentIntent** layer over Gateway: a persisted state machine, idempotency-key middleware, a reconciliation worker that re-drives hung intents, and an operator CLI. It fills the empty cell in Circle's SDK map — the Stablecoin Kit is stateless and USDCKit is custodial — which Circle cannot fill itself without cannibalizing CPN/StableFX.

**Cascade** — *Routing.* A 'USDC Anywhere' routing SDK: one-line `pay` / `quote` / `route` composing CCTP (Bridge Kit), Gateway, a StableFX quote, and x402. It wraps rather than rebuilds existing rails.

**Constellation** — *Agentic adapter.* A FacilitatorClient over `@circle-fin/x402-batching` so the official x402 middleware (express / fastify / hono / next) runs on Circle Nanopayments rails — bridging Circle's micropayments to the x402 standard.

**Meter** — *Agentic governance.* Seller-side nanopayment metering plus a buyer-side, persistent, wallet-decoupled spend-policy engine (budgets, velocity limits, kill-switch) — the safe-spend controls Circle's rails don't provide.

**Stream** — *Continuous payments.* Nanopayments-native continuous streaming — per-second salary, vesting, royalties — on the Gateway + Relay spine.

### Standalone Products

**Tideline (ArcScope)** — Stablecoin-flow intelligence — the first Arc-native payments analytics platform. A Rust enrichment service (`arc-stablecoin-stream`) adds semantic categorization on top of commodity event ingestion (Goldsky / Envio), stored in Postgres / TimescaleDB and surfaced in a Next.js dashboard. Incumbents like Dune and Nansen treat Arc as generic EVM; this treats it as a payment network.

**ArcNS** — An ENS-style naming service for Arc — human-readable `.arc` names with forward and reverse resolution on a three-layer registry / resolver architecture. Live at arcns-app.vercel.app.

**UPay / Tella** — A WhatsApp-based stablecoin payments app built on Circle Developer-Controlled Wallets, aimed at consumer payments and remittances (tella.cash). It is the built-in dogfood consumer of Relay.

**create-arc-app** — A CLI scaffolder (`npx create-arc-app`) that collapses Arc dapp setup — chain config, wallet wiring, USDC-as-native-gas handling — into one command, with selectable Next.js or Vite bases and optional Foundry contracts, wrapping Circle's Arc App Kit.

**B2B Invoicing** — A standalone business-invoicing product with on-chain settlement, deliberately decoupled from Relay by design so the two can evolve independently.

---

## Flagship Opportunities

The highest-scoring concepts from the catalog (**S** = strongest; full scoring in the workbook).

| Product | Domain | Tier |
|---|---|:--:|
| Confidential-transfer compliance & audit suite | Confidential Finance | S |
| Agent identity + reputation registry | Agentic Infrastructure | S |
| Agent spend-governance / policy engine | Agentic Infrastructure | A |
| ERC-3643-style transfer-restricted token framework | RWA and Compliance | A |
| Stripe-for-Arc merchant acceptance + hosted checkout | Payments and Activation | A |
| Permissionless regional stableswap AMM | FX and DeFi | A |
| Payment Alias / KYC-passport resolver | RWA and Compliance | A |
| Dispute & validator-action monitor | Trust and Verifiability | A |
| Blocklist-risk + escrow protection protocol | Trust and Verifiability | A |
| On/off-ramp aggregator + router (Africa-first) | Fiat-to-Crypto Boundary | A |

---

## Arc Weaknesses

The portfolio is built to attack these; codes are referenced throughout.

- **#1** — Cold-start — liquidity without real users
- **#2** — Centralization & trust — Circle-chosen validators, reversible transactions, freeze risk, PoS not due until 2028
- **#3** — Institution-first gap — SMB, emerging markets, developer experience, and the fiat-to-crypto boundary
- **#4** — Gated FX — StableFX is an institutional RFQ system; no permissionless AMM, no African pairs
- **#5** — Privacy ops gap — TEE-based confidential transfers shipped as a primitive, not tooled
- **#6** — Agentic adoption gap — rails exist, adoption is microscopic, standards fragmented
- **#7** — Token utility & governance still nascent
- **#8** — RWA & compliance composability is thin
