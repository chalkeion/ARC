# Arc Ecosystem — Product Catalog

A complete description of the products we are building and proposing on **Arc**, Circle's stablecoin-native L1 (USDC as native gas, mainnet beta targeting summer 2026). Every product here either attacks a specific weakness in Arc or amplifies one of its strengths; each is tagged with the weakness it addresses, a revenue model, and its first-mover edge.

This document is organized for the Arc / Circle team to read and filter. The companion workbook, `Arc_Ecosystem_Product_Opportunities_Ranked.xlsx`, holds the full scoring — first-mover strength, revenue potential, grant fundability, Arc strategic fit, and moat — across all entries.

**Status legend:** `In flight` = actively building, with code and in several cases live deployments. `Concept` = proposed, scored in the workbook. `Concept (R&D)` / `Concept (longer-horizon)` = heavier or research-stage.

---

## Table of Contents

- [Active Portfolio (In Flight)](#active-portfolio-in-flight)
  - [Payments Connective Tissue (Relay Cluster)](#payments-connective-tissue-relay-cluster)
  - [Standalone In-Flight Products](#standalone-in-flight-products)
- [Proposed Catalog by Domain](#proposed-catalog-by-domain)
  - [Confidential Finance](#confidential-finance) (6)
  - [Agentic Infrastructure](#agentic-infrastructure) (16)
  - [RWA and Compliance](#rwa-and-compliance) (15)
  - [FX and DeFi](#fx-and-defi) (21)
  - [Payments and Activation](#payments-and-activation) (20)
  - [Trust and Verifiability](#trust-and-verifiability) (6)
  - [Fiat-to-Crypto Boundary](#fiat-to-crypto-boundary) (7)
  - [Data and Analytics](#data-and-analytics) (3)
  - [Stablecoin Issuance](#stablecoin-issuance) (3)
  - [Cross-chain Infrastructure](#cross-chain-infrastructure) (3)
  - [Wallets and UX](#wallets-and-ux) (6)
  - [Developer Experience](#developer-experience) (7)
  - [Governance and Token](#governance-and-token) (6)
  - [Trade and Vertical](#trade-and-vertical) (5)
  - [Consumer and Emerging-Market Apps](#consumer-and-emerging-market-apps) (4)
- [Arc Weaknesses Reference](#arc-weaknesses-reference)

---

## Active Portfolio (In Flight)

The products already under construction — a connective-tissue payments stack plus standalone products. UPay dogfoods Relay; Tideline and ArcNS have live deployments.

### Payments Connective Tissue (Relay Cluster)

A composable, non-custodial payments stack on top of Circle's Stablecoin Kit that fills the gaps Circle's own SDKs leave open. (The `@usdkit/*` scope is retired — it collides with `@circle-fin/usdckit` — and a fresh scope is being chosen.)

**Gateway SDK** — *Foundation.* A typed Circle Gateway SDK — deposit, withdraw, unified-balance, burn-intent — with bounded retries and a discriminated-union error model. Everything else in the cluster builds on it.

**Relay** — *Spine.* A durable, non-custodial **PaymentIntent** layer over Gateway: a persisted state machine, idempotency-key middleware, a reconciliation worker that re-drives hung intents, and an operator CLI. It occupies the empty cell in Circle's SDK map — the Stablecoin Kit is stateless and USDCKit is custodial — and Circle cannot ship a durable OSS intent layer over its own non-custodial primitives without cannibalizing CPN/StableFX.

**Cascade** — *Routing.* A 'USDC Anywhere' routing SDK: one-line `pay` / `quote` / `route` composing CCTP (Bridge Kit), Gateway, a StableFX quote, and x402. It wraps rather than rebuilds existing rails.

**Constellation** — *Agentic adapter.* A FacilitatorClient over `@circle-fin/x402-batching` so the official x402 middleware (express / fastify / hono / next) runs on Circle Nanopayments rails — bridging Circle's micropayments to the x402 standard.

**Meter** — *Agentic governance.* Seller-side nanopayment metering plus a buyer-side, persistent, wallet-decoupled spend-policy engine (budgets, velocity limits, kill-switch) — the safe-spend controls Circle's rails don't provide.

**Stream** — *Continuous payments.* Nanopayments-native continuous streaming — per-second salary, vesting, royalties — on the Gateway + Relay spine.

### Standalone In-Flight Products

**Tideline (ArcScope)** — Stablecoin-flow intelligence — the first Arc-native payments analytics platform. A Rust enrichment service (`arc-stablecoin-stream`) adds semantic categorization on top of commodity event ingestion (Goldsky / Envio), stored in Postgres / TimescaleDB and surfaced in a Next.js dashboard. Incumbents like Dune and Nansen treat Arc as generic EVM; this treats it as a payment network.

**ArcNS** — An ENS-style naming service for Arc — human-readable `.arc` names with forward and reverse resolution on a three-layer registry / resolver architecture. Live at arcns-app.vercel.app.

**UPay / Tella** — A WhatsApp-based stablecoin payments app built on Circle Developer-Controlled Wallets, aimed at consumer payments and remittances (tella.cash). It is the built-in dogfood consumer of Relay.

**create-arc-app** — A CLI scaffolder (`npx create-arc-app`) that collapses Arc dapp setup — chain config, wallet wiring, USDC-as-native-gas handling — into one command, with selectable Next.js or Vite bases and optional Foundry contracts, wrapping Circle's Arc App Kit.

**B2B Invoicing** — A standalone business-invoicing product with on-chain settlement, deliberately decoupled from Relay by design so the two can evolve independently.

---

## Proposed Catalog by Domain

The broader slate, grouped by domain. In-flight projects above are not repeated here. Each entry lists the Arc weakness it addresses, a revenue model, its first-mover edge, and its tier from the companion workbook (S / A / B / C / D).

### Confidential Finance

*Operational tooling around Arc's TEE-based confidential transfers — the layer Circle ships as a primitive but leaves unbuilt. (Privacy ops gap, #5.)*

**Confidential-transfer compliance & audit suite** — View-key mgmt, auditor/regulator portal, selective-disclosure proof generation, encrypted-balance reconciliation.  
*Addresses:* Privacy tooling, Trust/decentralization · *Revenue:* Enterprise SaaS · *Edge:* Circle ships the primitive, not the ops tooling; enterprises can't operate confidential transfers without this. · *Tier:* S

**Confidential payroll (private amounts)** — Payroll where salary amounts are shielded via confidential transfers.  
*Addresses:* Privacy tooling, SMB/EM & DX · *Revenue:* Per-seat SaaS · *Edge:* A killer privacy use case named by Arc itself. · *Tier:* A

**Confidential B2B vendor-payment product** — Shielded vendor/supplier payments protecting commercial flows.  
*Addresses:* Privacy tooling · *Revenue:* SaaS / bps · *Edge:* Enterprise confidentiality demand. · *Tier:* A

**ZK address/graph-privacy complement** — ZK layer hiding addresses/graph (TEE hides amounts only).  
*Addresses:* Privacy tooling · *Revenue:* Grant / licensing · *Edge:* Roadmap gap; research-heavy, grant magnet. · *Tier:* B · *Status:* Concept (R&D)

**View-key management & rotation service** — Manage, rotate, and scope view keys for confidential accounts.  
*Addresses:* Privacy tooling · *Revenue:* SaaS · *Edge:* Foundational ops gap for privacy. · *Tier:* B

**Confidential treasury policy engine** — Automated treasury rules executing over shielded balances.  
*Addresses:* Privacy tooling · *Revenue:* SaaS · *Edge:* Combines privacy + automation; novel. · *Tier:* B

### Agentic Infrastructure

*The trust, governance, and interop layers above Circle's agent rails, where adoption is still microscopic and standards are fragmented. (Agentic adoption gap, #6.)*

**Agent identity + reputation registry** — Verifiable agent credentials, spend history, trust scores.  
*Addresses:* Agentic adoption · *Revenue:* Registry / API fees · *Edge:* Circle has wallets, no trust graph; network-effect moat. · *Tier:* S

**Agent spend-governance / policy engine** — Budgets, allowlists, velocity limits, approvals, kill-switch, audit trail for autonomous spend.  
*Addresses:* Agentic adoption, Cold-start · *Revenue:* SaaS · *Edge:* Circle owns rails, not policy; the safety layer agents need. · *Tier:* A

**Cross-standard payment router (x402<->AP2<->MPP)** — Adapter letting agents pay across fragmented standards.  
*Addresses:* Agentic adoption · *Revenue:* Usage fees · *Edge:* Standards war unresolved; interop is the gap. · *Tier:* A

**Agent-to-agent escrow / dispute layer** — Conditional escrow + dispute resolution for A2A commerce.  
*Addresses:* Agentic adoption · *Revenue:* % escrowed · *Edge:* Required as A2A volume grows. · *Tier:* B

**Know-Your-Agent (KYA) compliance layer** — Compliance/attestation for agents transacting value.  
*Addresses:* Agentic adoption, RWA/compliance · *Revenue:* SaaS · *Edge:* Regulators will demand it; first-mover. · *Tier:* B

**Agent spend reconciliation & accounting** — Aggregate thousands of nanopayments into invoices, ledgers, tax CSVs.  
*Addresses:* Agentic adoption · *Revenue:* SaaS · *Edge:* Nobody reconciles agent micro-spend. · *Tier:* B

**x402 paywall-as-a-service for sellers** — Turn any API/endpoint into a paid x402 resource in minutes.  
*Addresses:* Agentic adoption, Cold-start · *Revenue:* Take rate / SaaS · *Edge:* Supply-side monetization; Circle's marketplace is broad, dev-first niche open. · *Tier:* C

**Agent wallet SDK with hard risk-limits** — Wallet abstraction decoupled from Circle wallets, native spend caps.  
*Addresses:* Agentic adoption · *Revenue:* OSS + support · *Edge:* Alternative to Circle-locked wallets. · *Tier:* C

**Agent service marketplace / discovery** — Registry + discovery for agent-callable services, paid via x402.  
*Addresses:* Agentic adoption · *Revenue:* Take rate · *Edge:* Circle has a 'marketplace' — a dev-first niche stays open. · *Tier:* C

**Compute / inference payment rails** — Meter and settle GPU/inference usage for agents in USDC.  
*Addresses:* Agentic adoption · *Revenue:* bps · *Edge:* Core nanopayments use case. · *Tier:* C

**Nanopayment analytics / observability** — Dashboards + metrics for agent-commerce flows.  
*Addresses:* Agentic adoption · *Revenue:* SaaS · *Edge:* A new data category. · *Tier:* C

**Data marketplace for agents** — Sell datasets/feeds to agents per-call via nanopayments.  
*Addresses:* Agentic adoption · *Revenue:* Take rate · *Edge:* A new supply side. · *Tier:* C

**Agent-to-human payout bridge** — Let agents pay humans safely via off-ramp/card.  
*Addresses:* Agentic adoption · *Revenue:* bps · *Edge:* Closes the agent-economy loop. · *Tier:* C

**Machine subscription / standing-order for agents** — Recurring agent payments under policy.  
*Addresses:* Agentic adoption · *Revenue:* SaaS · *Edge:* Pairs with subscriptions + Meter. · *Tier:* C

**Prompt-to-payment guardrails / spend sandbox** — Simulate/limit agent spend before going live; safety sandbox.  
*Addresses:* Agentic adoption · *Revenue:* SaaS · *Edge:* Safety tooling; niche but timely. · *Tier:* D

**Agent SLA / quality-attestation layer** — Attest agent performance and SLAs.  
*Addresses:* Agentic adoption · *Revenue:* SaaS · *Edge:* Pairs with the reputation registry. · *Tier:* D

### RWA and Compliance

*Composable compliance, identity, and reconciliation primitives Arc invites but does not standardize. (RWA & compliance composability, #8.)*

**ERC-3643-style transfer-restricted token framework** — Permissioned-transfer token standard + claims/identity registry for Arc RWAs.  
*Addresses:* RWA/compliance, Trust/decentralization · *Revenue:* Licensing to issuers · *Edge:* Arc invites RWAs but lacks a composable compliance standard. · *Tier:* A

**Payment Alias / KYC-passport resolver** — Resolve an alias to a packet: KYC tier, multi-chain routing, Travel Rule endpoints, currency prefs.  
*Addresses:* RWA/compliance, SMB/EM & DX · *Revenue:* Per-resolution / SaaS · *Edge:* Your prior idea; an identity layer Circle won't own. · *Tier:* A

**Stablecoin-flow reconciliation engine** — Reconcile on-chain flows to ledgers for finance teams.  
*Addresses:* RWA/compliance, SMB/EM & DX · *Revenue:* SaaS · *Edge:* Enterprise back-office gap. · *Tier:* A · *Status:* Concept (early work)

**Transaction-monitoring / AML graph analytics** — Risk scoring and suspicious-flow detection on Arc.  
*Addresses:* Trust/decentralization, RWA/compliance · *Revenue:* SaaS · *Edge:* Institutions need it; first-mover on Arc. · *Tier:* A

**Travel Rule messaging / endpoint protocol** — Standard for exchanging Travel Rule data between Arc participants.  
*Addresses:* RWA/compliance · *Revenue:* SaaS / per-message · *Edge:* Compliance plumbing institutions need. · *Tier:* A

**Jurisdiction-aware compliance rules engine** — Policy engine encoding per-jurisdiction transfer rules.  
*Addresses:* RWA/compliance · *Revenue:* SaaS / licensing · *Edge:* A composable compliance backbone. · *Tier:* B

**On-chain KYC oracle** — Queryable attestation that an address or agent is KYC'd.  
*Addresses:* RWA/compliance, Agentic adoption · *Revenue:* Per-call · *Edge:* Reusable across apps and agents. · *Tier:* B

**RWA secondary market / compliant orderbook** — Trade tokenized RWAs with built-in privacy + transfer restrictions.  
*Addresses:* RWA/compliance, Privacy tooling · *Revenue:* Trading fees · *Edge:* A liquidity venue for idle RWAs. · *Tier:* B

**Whitelisted-transfer compliance middleware** — Drop-in modifier/library enforcing transfer rules.  
*Addresses:* RWA/compliance · *Revenue:* Licensing · *Edge:* Reusable across RWA issuers. · *Tier:* C

**Accredited-investor / eligibility verification** — Reusable accreditation credentials for RWA access.  
*Addresses:* RWA/compliance · *Revenue:* Per-verification · *Edge:* Gates RWA participation. · *Tier:* C

**Tokenized-asset issuance platform** — Issue/manage tokenized equities/funds/commodities with compliance + privacy.  
*Addresses:* RWA/compliance · *Revenue:* Setup + AUM bps · *Edge:* Crowded with institutions; differentiate on tooling. · *Tier:* C

**RWA collateral oracle / NAV attestation** — Attested NAV/price feeds for RWA collateral.  
*Addresses:* RWA/compliance, Trust/decentralization · *Revenue:* Data fees · *Edge:* Enables RWA lending. · *Tier:* C

**Regulatory-reporting automation** — Auto-generate compliance/regulatory reports from Arc activity.  
*Addresses:* RWA/compliance · *Revenue:* SaaS · *Edge:* Back-office gap. · *Tier:* C

**Cap-table / securities registry** — On-chain cap-table + transfer-agent functions.  
*Addresses:* RWA/compliance · *Revenue:* SaaS · *Edge:* Niche; regulated. · *Tier:* C

**Tax-lot / cost-basis accounting for Arc** — Cost-basis and tax reporting for Arc holdings and flows.  
*Addresses:* RWA/compliance, SMB/EM & DX · *Revenue:* SaaS · *Edge:* Distinct from the USDC-gas tax tool. · *Tier:* C

### FX and DeFi

*Permissionless liquidity and FX for the long-tail and regional pairs StableFX's institutional RFQ won't serve. (Gated FX, #4.)*

**Permissionless regional stableswap AMM** — AMM for long-tail/regional pairs StableFX won't list (NGN/KES/GHS <-> USDC).  
*Addresses:* Permissionless FX, Cold-start · *Revenue:* Swap fees + LP · *Edge:* StableFX is RFQ/institution-gated; this lane is wide open. · *Tier:* A

**Smart FX router (StableFX RFQ + AMM aggregation)** — Best-execution router across StableFX quotes and AMM pools.  
*Addresses:* Permissionless FX · *Revenue:* Routing spread · *Edge:* Sits above both — turns the RFQ critique into a product. · *Tier:* A

**FX forwards / hedging primitive** — On-chain FX forwards and NDFs for stablecoin pairs.  
*Addresses:* Permissionless FX · *Revenue:* Spread / fees · *Edge:* Treasuries need hedging; novel on Arc. · *Tier:* A

**Prediction markets platform** — Capital-efficient prediction markets with instant USDC settlement.  
*Addresses:* Cold-start · *Revenue:* Trading fees · *Edge:* Arc explicitly names this a target use case — first-mover. · *Tier:* B

**StableFX market-maker / quoting-bot framework** — SDK + infra for market makers to quote StableFX RFQ programmatically.  
*Addresses:* Permissionless FX · *Revenue:* SaaS / rev-share · *Edge:* Supply-side enabler for StableFX liquidity. · *Tier:* B

**Per-country regional stablecoin issuance (NGN/KES/GHS/EGP/ZAR)** — Issue and maintain country stablecoins bridged to Arc.  
*Addresses:* SMB/EM & DX, Permissionless FX · *Revenue:* Float / fees · *Edge:* African coverage gap StableFX ignores. · *Tier:* B

**USYC-collateral lending/borrowing protocol** — Lending markets using USDC/USYC as collateral.  
*Addresses:* Cold-start, RWA/compliance · *Revenue:* Spread / fees · *Edge:* Activates idle institutional assets. · *Tier:* B

**Undercollateralized institutional credit** — KYC-gated credit lines on Arc.  
*Addresses:* RWA/compliance, Cold-start · *Revenue:* Spread · *Edge:* Matches Arc's 'onchain credit platform' positioning. · *Tier:* B

**NDF for restricted / capital-controlled currencies** — Non-deliverable forwards for restricted FX.  
*Addresses:* Permissionless FX · *Revenue:* Spread · *Edge:* Emerging-market corridor edge; complex. · *Tier:* B

**Consumer savings / money-market product** — Yield-bearing USDC savings (USYC-backed) for consumers/SMB.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* Mgmt fee / spread · *Edge:* Demand-side adoption driver. · *Tier:* C

**Structured products on USYC** — Principal-protected / yield-enhanced notes on USYC.  
*Addresses:* RWA/compliance, Cold-start · *Revenue:* Mgmt fee · *Edge:* Institutional appetite. · *Tier:* C

**Perp / derivatives DEX (stablecoin pairs/indices)** — Perps on FX pairs and stablecoin indices.  
*Addresses:* Permissionless FX, Cold-start · *Revenue:* Trading fees · *Edge:* Activity driver; competitive category. · *Tier:* C

**Concentrated-liquidity stableswap (Curve-style)** — Capital-efficient stable AMM tuned for pegged pairs.  
*Addresses:* Permissionless FX · *Revenue:* Swap fees · *Edge:* DeFi primitive; competitive category. · *Tier:* C

**Native FX / price oracle (stablecoin-tuned)** — Oracle for regional FX rates and RWA NAV on Arc.  
*Addresses:* Permissionless FX, RWA/compliance · *Revenue:* Data fees · *Edge:* Chainlink is generic; an FX-specific niche is open. · *Tier:* C

**Liquidity-as-a-service / LP vault manager** — Automated LP strategies for stableswap/StableFX.  
*Addresses:* Permissionless FX, Cold-start · *Revenue:* Perf/mgmt fee · *Edge:* Bootstraps the AMM you build. · *Tier:* C

**Stable yield aggregator / vault router** — Auto-allocate USDC across Arc yield venues.  
*Addresses:* Cold-start · *Revenue:* Perf fee · *Edge:* Demand-side yield. · *Tier:* C

**Interest-rate / FX swap protocol** — On-chain swaps for rate and FX exposure.  
*Addresses:* Permissionless FX, RWA/compliance · *Revenue:* Fees · *Edge:* Advanced, institutional. · *Tier:* C

**Insurance / cover protocol** — Cover for smart-contract, freeze, or depeg risk.  
*Addresses:* Trust/decentralization, Cold-start · *Revenue:* Premiums · *Edge:* Pairs with freeze-insurance. · *Tier:* C

**Multi-hop FX routing engine** — Route through intermediate pairs for best cross-rate.  
*Addresses:* Permissionless FX · *Revenue:* Spread · *Edge:* Extends the smart FX router. · *Tier:* C

**Liquidation-bot / keeper infrastructure** — Keeper network for lending liquidations on Arc.  
*Addresses:* Cold-start · *Revenue:* Fees · *Edge:* Infra for the lending cluster. · *Tier:* D

**FX rate index / benchmark product** — Published on-chain stablecoin FX index.  
*Addresses:* Permissionless FX · *Revenue:* Licensing / data · *Edge:* A reference-rate play. · *Tier:* D

### Payments and Activation

*Rails that manufacture real, recurring on-chain activity to counter the empty-chain problem. (Cold-start #1, SMB/EM gap #3.)*

**Stripe-for-Arc merchant acceptance + hosted checkout** — Accept USDC, auto-FX to a local stablecoin, hosted checkout + payout/off-ramp.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* Processing bps · *Edge:* Direct attack on empty-chain + fiat boundary — Codex's whole thesis. · *Tier:* A

**Remittance corridor app (Lagos to China/Gulf/UK)** — USDC-rail remittance with local cash-in/out; your Konfide corridor DNA on a chain built for it.  
*Addresses:* SMB/EM & DX, Cold-start · *Revenue:* FX spread + fee · *Edge:* Emerging-market corridors underserved; real recurring volume. · *Tier:* A

**Subscriptions / recurring-billing primitive** — Native scheduler + USDC pull-payment mandates + dashboard.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* SaaS + bps · *Edge:* Circle ships a paymaster, not subscription UX/mandates. · *Tier:* B

**Non-custodial refund/chargeback protocol** — Programmable refund/partial-refund + dispute primitive for merchants.  
*Addresses:* Cold-start, Trust/decentralization · *Revenue:* Integration fee · *Edge:* Stablecoins lack chargebacks; merchants need them. · *Tier:* B

**On-chain invoicing + AR/AP** — Invoice issue/track/settle in USDC with reminders + off-ramp for SMB/freelancers.  
*Addresses:* SMB/EM & DX, Cold-start · *Revenue:* Per-invoice / % volume; SaaS · *Edge:* No Arc-native AR/AP. · *Tier:* C

**Payroll product** — Multi-employee USDC payroll, scheduling, off-ramp, optional confidential amounts.  
*Addresses:* SMB/EM & DX, Cold-start · *Revenue:* Per-seat/per-run SaaS · *Edge:* Recurring volume; emerging-market angle. · *Tier:* C

**Bill-pay / utility-payment rails (EM)** — Pay utilities/airtime/bills from USDC in emerging markets.  
*Addresses:* SMB/EM & DX, Cold-start · *Revenue:* bps / biller commissions · *Edge:* Real-world emerging-market utility. · *Tier:* C

**BNPL / pay-in-installments** — Installment payments with on-chain schedules.  
*Addresses:* Cold-start · *Revenue:* Merchant fee / interest · *Edge:* Novel on Arc; carries credit risk. · *Tier:* C

**Expense management / corporate-card ops** — Track, categorize, reconcile USDC card/agent spend for businesses.  
*Addresses:* SMB/EM & DX · *Revenue:* SaaS · *Edge:* Pairs with card-issuing. · *Tier:* C

**E-commerce platform plugins (Shopify/Woo)** — Drop-in USDC checkout for major commerce platforms.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* bps · *Edge:* Distribution; complements Stripe-for-Arc. · *Tier:* C

**Gig-worker / marketplace instant payout** — Instant USDC payouts for gig and marketplace platforms.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* bps · *Edge:* Real recurring volume. · *Tier:* C

**Atomic split-payments / revenue-share router** — Atomic multi-party splits (your GoodDistributor pattern) for platforms/creators.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* bps / licensing · *Edge:* Reusable primitive; marketplaces need it. · *Tier:* C · *Status:* Concept (early work)

**Treasury sweep / auto-rebalance automation** — Rules to sweep idle USDC into yield/treasury, cross-chain.  
*Addresses:* SMB/EM & DX · *Revenue:* SaaS / bps · *Edge:* Built on Gateway unified balance. · *Tier:* C

**Payment links / POS app** — Merchant payment links + QR POS for in-person/online USDC.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* bps / SaaS · *Edge:* Drives real merchant transactions. · *Tier:* C

**Embeddable 'Pay with USDC' widget SDK** — Drop-in button/checkout component (React/JS) wrapping App Kit + Relay.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* OSS + hosted bps · *Edge:* Distribution play; few polished Arc widgets. · *Tier:* C

**Subscription dunning / smart-retry engine** — Retry failed pull-payments and recover churn.  
*Addresses:* Cold-start · *Revenue:* SaaS / % recovered · *Edge:* Pairs with subscriptions + Relay. · *Tier:* C

**Payment-request / QR standard + SDK** — Standardized pay-request URIs/QR for Arc USDC.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* OSS to grant · *Edge:* An interop primitive the ecosystem lacks. · *Tier:* D

**Escrow-as-a-service** — Milestone/condition escrow for marketplaces/freelance.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* % of escrowed · *Edge:* Team note: basic escrow already exists — must differentiate. · *Tier:* D · *Status:* Concept (early work)

**Creator monetization / tipping rails** — Tips, paid content, fan payments in USDC + nanopayments.  
*Addresses:* Cold-start · *Revenue:* Take rate · *Edge:* Consumer activity driver. · *Tier:* D

**Donation / fundraising rails** — Transparent on-chain donations with receipts.  
*Addresses:* Cold-start · *Revenue:* Small fee / SaaS · *Edge:* NGO and emerging-market angle. · *Tier:* D

### Trust and Verifiability

*Tooling that makes a consortium chain safe to integrate against — monitoring, freeze protection, transparency. (Centralization & trust, #2.)*

**Dispute & validator-action monitor** — Real-time alerts on tx reversals, validator rotation, blocklist/freeze events; integrator-grade.  
*Addresses:* Trust/decentralization · *Revenue:* Alerts API / SaaS · *Edge:* Nobody watches consortium behavior; integrators need it to trust Arc. · *Tier:* A

**Blocklist-risk + escrow protection protocol** — Contract library routing a frozen address's positions into escrow instead of bricking the protocol for all users.  
*Addresses:* Trust/decentralization · *Revenue:* Integration fee / % protected TVL · *Edge:* Direct freeze-risk mitigation; your prior concept, still unbuilt. · *Tier:* A

**Proof-of-reserves / attestation dashboard** — Verifiable reserve/attestation display for Arc-issued tokenized assets.  
*Addresses:* Trust/decentralization, RWA/compliance · *Revenue:* SaaS to issuers · *Edge:* RWA issuers need a trust surface. · *Tier:* C

**Validator transparency / decentralization scoreboard** — Public scoreboard tracking validator diversity, rotation, uptime, jurisdiction.  
*Addresses:* Trust/decentralization · *Revenue:* Grant / sponsorship; data API · *Edge:* Counters the loudest critique narrative; foundation-aligned. · *Tier:* C

**Pre-tx screening service (OFAC/blocklist)** — Non-custodial API to check addresses against blocklist/sanctions before sending.  
*Addresses:* Trust/decentralization, SMB/EM & DX · *Revenue:* API / SaaS · *Edge:* Compliance utility; reduces freeze surprises. · *Tier:* C

**Freeze-insurance / blocklist hedging** — Risk product covering USDC freeze exposure for treasuries.  
*Addresses:* Trust/decentralization · *Revenue:* Premiums · *Edge:* Novel; capital-intensive and regulated. · *Tier:* D · *Status:* Concept (longer-horizon)

### Fiat-to-Crypto Boundary

*The fiat-to-crypto edge — the real bottleneck — with an emerging-market, Africa-first focus. (Institution-first gap, #3.)*

**On/off-ramp aggregator + router (Africa-first)** — Route across ramp providers for best rate; reuse KYC; Arc-settled.  
*Addresses:* SMB/EM & DX, Cold-start · *Revenue:* bps · *Edge:* Thin emerging-market ramp coverage — the real bottleneck. · *Tier:* A

**Reusable KYC-passport across ramps** — Portable verified-identity credential reused across ramps/apps.  
*Addresses:* SMB/EM & DX, RWA/compliance · *Revenue:* Per-verification / SaaS · *Edge:* Cuts onboarding friction; identity moat. · *Tier:* B

**Mobile-money bridge (M-Pesa/Opay/MoMo <-> USDC)** — Connect mobile-money wallets to Arc USDC in/out.  
*Addresses:* SMB/EM & DX, Cold-start · *Revenue:* bps / commissions · *Edge:* Emerging-market cash-in/out is the adoption moat. · *Tier:* B

**Cash agent-network coordination layer** — Coordinate human cash-in/out agents (liquidity, settlement, reputation).  
*Addresses:* SMB/EM & DX, Cold-start · *Revenue:* Take rate · *Edge:* Last-mile EM liquidity; hard and defensible. · *Tier:* B

**Local-stablecoin issuance + Arc-bridge toolkit** — Tooling to issue cNGN-class local stablecoins and bridge/list them on Arc.  
*Addresses:* SMB/EM & DX, Permissionless FX · *Revenue:* Licensing / setup · *Edge:* No African stablecoins on Arc yet. · *Tier:* B

**Virtual-account / IBAN issuance for USDC** — Issue a bank account/IBAN that settles to USDC on Arc.  
*Addresses:* SMB/EM & DX · *Revenue:* Per-account / bps · *Edge:* Bridges TradFi rails; partner-heavy. · *Tier:* C

**Card-issuing bridge (spend USDC via card)** — Issue cards that draw from an Arc USDC balance.  
*Addresses:* SMB/EM & DX · *Revenue:* Interchange · *Edge:* Real-world spend; partner/regulatory heavy. · *Tier:* C

### Data and Analytics

*Payments-native intelligence on top of raw indexers, which now exist but stop at generic EVM data. (Cold-start #1, RWA/compliance #8.)*

**Address labeling / entity resolution** — Label entities, exchanges, and contracts on Arc.  
*Addresses:* Trust/decentralization, RWA/compliance · *Revenue:* Data API · *Edge:* Powers AML and analytics. · *Tier:* C

**Merchant / payments analytics** — Revenue, settlement, and refund analytics for Arc merchants.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* SaaS · *Edge:* Pairs with checkout. · *Tier:* C

**Stablecoin rate / yield dashboard** — Compare yields and rates across Arc venues.  
*Addresses:* Cold-start · *Revenue:* Freemium / leads · *Edge:* Demand-side discovery. · *Tier:* D

### Stablecoin Issuance

*Tooling to bring new issuers, currencies, and liquidity onto Arc. (Institution-first gap #3, cold-start #1.)*

**Stablecoin-issuance-as-a-service (white-label)** — Launch your own compliant stablecoin on Arc — mint, redeem, reserve attestation.  
*Addresses:* SMB/EM & DX, Cold-start · *Revenue:* Setup + bps · *Edge:* Brings new issuers and liquidity onto Arc. · *Tier:* A

**Tokenized-deposit issuance for banks** — Tooling for banks to issue tokenized deposits on Arc.  
*Addresses:* RWA/compliance · *Revenue:* Licensing · *Edge:* An institutional onramp; partner-heavy. · *Tier:* B

**Yield-bearing stablecoin wrapper** — Wrap USDC into a yield-bearing (USYC-backed) token with clean UX.  
*Addresses:* Cold-start · *Revenue:* Spread · *Edge:* A demand-side yield primitive. · *Tier:* C

### Cross-chain Infrastructure

*Orchestration that realizes Arc's settlement-hub thesis across CCTP and Gateway. (Institution-first gap, #3.)*

**Arc-as-hub omnichain treasury rebalancer** — Omnichain USDC balance manager using CCTP/Gateway.  
*Addresses:* SMB/EM & DX · *Revenue:* SaaS / bps · *Edge:* Realizes Arc's settlement-hub thesis. · *Tier:* B

**Omnichain stablecoin SDK** — One SDK to manage USDC balances/transfers across chains incl. Arc.  
*Addresses:* SMB/EM & DX · *Revenue:* OSS + support · *Edge:* Frame as balance-management vs Cascade's routing. · *Tier:* C

**CCTP / bridge analytics + monitor** — Monitor cross-chain USDC flows and bridge health with alerts.  
*Addresses:* Trust/decentralization, SMB/EM & DX · *Revenue:* SaaS · *Edge:* An operational trust surface. · *Tier:* C

### Wallets and UX

*Embedded wallets, recovery, and policy controls tuned to Arc's USDC-gas and confidential model. (Institution-first / DX gap, #3.)*

**Wallet-as-a-Service (white-label embedded wallets)** — Embeddable, branded self-custodial wallets for any Arc app — passkeys, recovery, gas sponsorship.  
*Addresses:* SMB/EM & DX · *Revenue:* SaaS / per-MAU · *Edge:* Blockscout teases WaaS; a dev-first, Arc-tuned lane is open. · *Tier:* B

**Treasury multisig / policy wallet** — Multisig + spending policies for org treasuries — USDC-gas and confidential-aware.  
*Addresses:* SMB/EM & DX, Trust/decentralization · *Revenue:* SaaS / per-seat · *Edge:* Safe-style but purpose-built for Arc. · *Tier:* C

**Batch-payment / mass-payout UI + SDK** — CSV-to-batch USDC payouts with retries and receipts.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* SaaS / bps · *Edge:* Payroll, airdrops, vendor runs — drives volume. · *Tier:* C

**Social-recovery / account-recovery module** — Guardian-based recovery for Arc smart accounts.  
*Addresses:* SMB/EM & DX · *Revenue:* OSS + SaaS · *Edge:* Cuts key-loss churn; reusable primitive. · *Tier:* C

**In-wallet swap / FX widget** — Embedded swap routing StableFX + AMM inside any wallet.  
*Addresses:* Permissionless FX, SMB/EM & DX · *Revenue:* bps · *Edge:* Distribution surface for the FX router. · *Tier:* D

**Address book / payment-identity contacts** — Human-readable contacts wired to Payment Alias.  
*Addresses:* SMB/EM & DX · *Revenue:* Freemium · *Edge:* UX glue across the payments stack. · *Tier:* D

### Developer Experience

*Runtime, debugging, and testing tools beyond Circle's first-party scaffolding. (Institution-first / DX gap, #3.)*

**TEE / confidential-transfer testing harness** — Local devnet + tooling to test confidential transfers/view keys.  
*Addresses:* Privacy tooling, SMB/EM & DX · *Revenue:* OSS + SaaS · *Edge:* Privacy is hard to test; nobody's tooling it. · *Tier:* B

**ArcLens — observability + error-decoding + tx simulation SDK** — Human-readable error decoding, preflight simulation, smart RPC routing for Arc.  
*Addresses:* SMB/EM & DX · *Revenue:* OSS to grant; paid tiers · *Edge:* Your StellarLens/MonadLens port; DX gap beyond Circle's kits. · *Tier:* B

**Arc MCP server (LLM-queryable data + actions)** — MCP server exposing Arc data/actions to LLMs/agents.  
*Addresses:* SMB/EM & DX, Agentic adoption · *Revenue:* OSS to grant; SaaS · *Edge:* Rides agentic + dev tooling; novel. · *Tier:* B

**Account-abstraction / smart-wallet SDK** — Passkeys, session keys, gas-sponsorship policies on Arc.  
*Addresses:* SMB/EM & DX · *Revenue:* OSS + enterprise · *Edge:* Competes with Circle wallets — differentiate on policy/AA. · *Tier:* C

**App-level webhook / event-stream layer** — Semantic webhooks on top of indexers (payment received, intent settled).  
*Addresses:* SMB/EM & DX, Cold-start · *Revenue:* SaaS · *Edge:* Indexers ship raw data, not app-level events. · *Tier:* C

**Foundry/Hardhat plugin for Arc** — Blockscout verify, USDC-gas-aware gas reports, Arc presets.  
*Addresses:* SMB/EM & DX · *Revenue:* OSS to grant · *Edge:* Smooths the verify pain your spike surfaced. · *Tier:* C

**Stablecoin contract-template library** — Audited templates: payments, escrow, streaming, splits, subscriptions.  
*Addresses:* SMB/EM & DX · *Revenue:* OSS to grant; support · *Edge:* Accelerates builders; ecosystem-aligned. · *Tier:* D

### Governance and Token

*Accounting, governance, and staking tooling for ARC's still-undefined utility and the PoS transition. (Token & governance nascent, #7.)*

**USDC-gas tax & accounting tool** — Track/report USDC-as-gas for tax and books (gas-in-stablecoin is messy).  
*Addresses:* Token/governance, SMB/EM & DX · *Revenue:* SaaS · *Edge:* Unsolved accounting quirk unique to Arc. · *Tier:* C

**ARC liquid-staking token (post-PoS)** — An LST for staked ARC.  
*Addresses:* Token/governance · *Revenue:* Mgmt fee / spread · *Edge:* Big if PoS lands; future-dated and competitive. · *Tier:* C · *Status:* Concept (longer-horizon)

**Governance/delegate dashboard + Treasury analytics** — Track proposals, delegate, analyze the on-chain Arc Treasury (fees flow there).  
*Addresses:* Token/governance · *Revenue:* SaaS / grant · *Edge:* Governance is new; the treasury is real and on-chain. · *Tier:* C

**Validator-ops / node-monitoring suite** — Monitoring/alerting/ops for Arc validators.  
*Addresses:* Token/governance, Trust/decentralization · *Revenue:* SaaS to validators · *Edge:* Small operator set initially. · *Tier:* D

**Staking / delegation tooling (post-PoS)** — Staking, delegation, rewards UX for the PoS transition.  
*Addresses:* Token/governance · *Revenue:* Commission / SaaS · *Edge:* Foundation may absorb this — timing risk. · *Tier:* D

**Gas-budgeting / fee-forecasting tool** — Forecast USDC fees (EIP-1559 moving-average aware) for budgeting.  
*Addresses:* Token/governance, SMB/EM & DX · *Revenue:* SaaS · *Edge:* Niche but useful for high-volume apps. · *Tier:* D

### Trade and Vertical

*Vertical settlement and financing — trade finance, factoring, marketplaces, DAOs. (Cold-start #1, RWA/compliance #8.)*

**Trade finance / supply-chain finance** — On-chain letters of credit and PO financing settled in USDC.  
*Addresses:* RWA/compliance, Cold-start · *Revenue:* Fees / spread · *Edge:* A large TradFi corridor; complex. · *Tier:* B

**Invoice factoring / receivables financing** — Advance against on-chain invoices.  
*Addresses:* Cold-start, RWA/compliance · *Revenue:* Discount / spread · *Edge:* Pairs with invoicing. · *Tier:* C

**B2B marketplace settlement layer** — Settlement, escrow, and reconciliation for B2B marketplaces.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* bps · *Edge:* A platform play. · *Tier:* C

**DAO payroll / contributor payments** — Streaming, batch payments, and compliance for DAOs.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* SaaS · *Edge:* Pairs with Stream. · *Tier:* C

**Real-estate / commodities settlement** — Settlement and escrow for tokenized real assets.  
*Addresses:* RWA/compliance · *Revenue:* Fees · *Edge:* An RWA vertical. · *Tier:* D

### Consumer and Emerging-Market Apps

*Demand-side consumer and emerging-market apps that bring real users on-chain. (Cold-start #1, SMB/EM gap #3.)*

**SMB neobank on Arc rails** — Business accounts, payments, payroll, FX for SMBs.  
*Addresses:* SMB/EM & DX, Cold-start · *Revenue:* SaaS + bps · *Edge:* Bundles many rails; large but heavy. · *Tier:* C

**Consumer USDC wallet w/ local-currency UX + ramps** — Mobile wallet showing local currency, built-in ramps, Africa-first.  
*Addresses:* SMB/EM & DX, Cold-start · *Revenue:* bps / premium · *Edge:* Demand-side adoption; competitive but the EM lane is open. · *Tier:* D

**Savings-circle / ROSCA (esusu/ajo) dapp** — Digitize rotating savings circles with USDC.  
*Addresses:* Cold-start, SMB/EM & DX · *Revenue:* Small fee · *Edge:* Culturally-rooted EM activity driver. · *Tier:* D

**Bill-splitting / P2P consumer app** — Social P2P payments + splitting in USDC.  
*Addresses:* Cold-start · *Revenue:* Premium / interchange · *Edge:* Consumer activity; crowded. · *Tier:* D

## Arc Weaknesses Reference

The catalog is built to attack these. Codes (#1–#8) are referenced throughout.

- **#1** — Cold-start — liquidity without real users (stablecoin chains have TVL but almost no transactional activity)
- **#2** — Centralization & trust concentration — Circle-chosen validators, reversible via dispute protocols, USDC freeze risk, PoS not due until 2028
- **#3** — Institution-first gap — SMB, emerging markets, developer experience, and the fiat<->crypto boundary (the real bottleneck)
- **#4** — Gated FX — StableFX is an institutional RFQ system; no permissionless AMM and no African pairs
- **#5** — Privacy ops gap — TEE-based confidential transfers ship as a primitive, not as operable tooling
- **#6** — Agentic adoption gap — rails exist, adoption is microscopic, and standards (x402 / AP2 / MPP) are fragmented
- **#7** — Token utility & governance still nascent
- **#8** — RWA & compliance composability is thin
