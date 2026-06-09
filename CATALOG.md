# Arc Ecosystem — Full Product Catalog

The complete proposed slate, grouped by domain. In-flight projects are described in the [README](README.md); full scoring (first-mover, revenue, grant-fit, Arc-fit, moat) lives in `Arc_Ecosystem_Product_Opportunities_Ranked.xlsx`.

**Tiers** rank each concept on a weighted blend of those scores: **S** exceptional · **A** strong · **B** solid · **C** situational · **D** weak.

### Contents

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

---

## Confidential Finance

> Operational tooling around Arc's TEE-based confidential transfers — shipped by Circle as a primitive, not as operable tooling.

| Product | What it is | Tier |
|---|---|:--:|
| Confidential-transfer compliance & audit suite | View-key mgmt, auditor/regulator portal, selective-disclosure proof generation, encrypted-balance reconciliation. | S |
| Confidential B2B vendor-payment product | Shielded vendor/supplier payments protecting commercial flows. | A |
| Confidential payroll (private amounts) | Payroll where salary amounts are shielded via confidential transfers. | A |
| ZK address/graph-privacy complement | ZK layer hiding addresses/graph (TEE hides amounts only). | B |
| Confidential treasury policy engine | Automated treasury rules executing over shielded balances. | B |
| View-key management & rotation service | Manage, rotate, and scope view keys for confidential accounts. | B |

---

## Agentic Infrastructure

> The trust, governance, and interop layers above Circle's agent rails, where adoption is microscopic and standards are fragmented.

| Product | What it is | Tier |
|---|---|:--:|
| Agent identity + reputation registry | Verifiable agent credentials, spend history, trust scores. | S |
| Agent spend-governance / policy engine | Budgets, allowlists, velocity limits, approvals, kill-switch, audit trail for autonomous spend. | A |
| Cross-standard payment router (x402<->AP2<->MPP) | Adapter letting agents pay across fragmented standards. | A |
| Agent-to-agent escrow / dispute layer | Conditional escrow + dispute resolution for A2A commerce. | B |
| Know-Your-Agent (KYA) compliance layer | Compliance/attestation for agents transacting value. | B |
| Agent spend reconciliation & accounting | Aggregate thousands of nanopayments into invoices, ledgers, tax CSVs. | B |
| Agent service marketplace / discovery | Registry + discovery for agent-callable services, paid via x402. | C |
| Agent wallet SDK with hard risk-limits | Wallet abstraction decoupled from Circle wallets, native spend caps. | C |
| Compute / inference payment rails | Meter and settle GPU/inference usage for agents in USDC. | C |
| x402 paywall-as-a-service for sellers | Turn any API/endpoint into a paid x402 resource in minutes. | C |
| Agent-to-human payout bridge | Let agents pay humans safely via off-ramp/card. | C |
| Data marketplace for agents | Sell datasets/feeds to agents per-call via nanopayments. | C |
| Machine subscription / standing-order for agents | Recurring agent payments under policy. | C |
| Nanopayment analytics / observability | Dashboards + metrics for agent-commerce flows. | C |
| Agent SLA / quality-attestation layer | Attest agent performance and SLAs. | D |
| Prompt-to-payment guardrails / spend sandbox | Simulate/limit agent spend before going live; safety sandbox. | D |

---

## RWA and Compliance

> Composable compliance, identity, and reconciliation primitives Arc invites but does not standardize.

| Product | What it is | Tier |
|---|---|:--:|
| ERC-3643-style transfer-restricted token framework | Permissioned-transfer token standard + claims/identity registry for Arc RWAs. | A |
| Payment Alias / KYC-passport resolver | Resolve an alias to a packet: KYC tier, multi-chain routing, Travel Rule endpoints, currency prefs. | A |
| Stablecoin-flow reconciliation engine | Reconcile on-chain flows to ledgers for finance teams. | A |
| Transaction-monitoring / AML graph analytics | Risk scoring and suspicious-flow detection on Arc. | A |
| Travel Rule messaging / endpoint protocol | Standard for exchanging Travel Rule data between Arc participants. | A |
| Jurisdiction-aware compliance rules engine | Policy engine encoding per-jurisdiction transfer rules. | B |
| On-chain KYC oracle | Queryable attestation that an address or agent is KYC'd. | B |
| RWA secondary market / compliant orderbook | Trade tokenized RWAs with built-in privacy + transfer restrictions. | B |
| Accredited-investor / eligibility verification | Reusable accreditation credentials for RWA access. | C |
| Whitelisted-transfer compliance middleware | Drop-in modifier/library enforcing transfer rules. | C |
| Regulatory-reporting automation | Auto-generate compliance/regulatory reports from Arc activity. | C |
| RWA collateral oracle / NAV attestation | Attested NAV/price feeds for RWA collateral. | C |
| Tokenized-asset issuance platform | Issue/manage tokenized equities/funds/commodities with compliance + privacy. | C |
| Cap-table / securities registry | On-chain cap-table + transfer-agent functions. | C |
| Tax-lot / cost-basis accounting for Arc | Cost-basis and tax reporting for Arc holdings and flows. | C |

---

## FX and DeFi

> Permissionless liquidity and FX for the long-tail and regional pairs StableFX's institutional RFQ won't serve.

| Product | What it is | Tier |
|---|---|:--:|
| Permissionless regional stableswap AMM | AMM for long-tail/regional pairs StableFX won't list (NGN/KES/GHS <-> USDC). | A |
| FX forwards / hedging primitive | On-chain FX forwards and NDFs for stablecoin pairs. | A |
| Smart FX router (StableFX RFQ + AMM aggregation) | Best-execution router across StableFX quotes and AMM pools. | A |
| Prediction markets platform | Capital-efficient prediction markets with instant USDC settlement. | B |
| Per-country regional stablecoin issuance (NGN/KES/GHS/EGP/ZAR) | Issue and maintain country stablecoins bridged to Arc. | B |
| StableFX market-maker / quoting-bot framework | SDK + infra for market makers to quote StableFX RFQ programmatically. | B |
| Undercollateralized institutional credit | KYC-gated credit lines on Arc. | B |
| USYC-collateral lending/borrowing protocol | Lending markets using USDC/USYC as collateral. | B |
| NDF for restricted / capital-controlled currencies | Non-deliverable forwards for restricted FX. | B |
| Consumer savings / money-market product | Yield-bearing USDC savings (USYC-backed) for consumers/SMB. | C |
| Perp / derivatives DEX (stablecoin pairs/indices) | Perps on FX pairs and stablecoin indices. | C |
| Structured products on USYC | Principal-protected / yield-enhanced notes on USYC. | C |
| Concentrated-liquidity stableswap (Curve-style) | Capital-efficient stable AMM tuned for pegged pairs. | C |
| Native FX / price oracle (stablecoin-tuned) | Oracle for regional FX rates and RWA NAV on Arc. | C |
| Insurance / cover protocol | Cover for smart-contract, freeze, or depeg risk. | C |
| Interest-rate / FX swap protocol | On-chain swaps for rate and FX exposure. | C |
| Liquidity-as-a-service / LP vault manager | Automated LP strategies for stableswap/StableFX. | C |
| Multi-hop FX routing engine | Route through intermediate pairs for best cross-rate. | C |
| Stable yield aggregator / vault router | Auto-allocate USDC across Arc yield venues. | C |
| FX rate index / benchmark product | Published on-chain stablecoin FX index. | D |
| Liquidation-bot / keeper infrastructure | Keeper network for lending liquidations on Arc. | D |

---

## Payments and Activation

> Rails that manufacture real, recurring on-chain activity to counter the empty-chain problem.

| Product | What it is | Tier |
|---|---|:--:|
| Stripe-for-Arc merchant acceptance + hosted checkout | Accept USDC, auto-FX to a local stablecoin, hosted checkout + payout/off-ramp. | A |
| Remittance corridor app (Lagos to China/Gulf/UK) | USDC-rail remittance with local cash-in/out; your Konfide corridor DNA on a chain built for it. | A |
| Subscriptions / recurring-billing primitive | Native scheduler + USDC pull-payment mandates + dashboard. | B |
| Non-custodial refund/chargeback protocol | Programmable refund/partial-refund + dispute primitive for merchants. | B |
| Bill-pay / utility-payment rails (EM) | Pay utilities/airtime/bills from USDC in emerging markets. | C |
| BNPL / pay-in-installments | Installment payments with on-chain schedules. | C |
| E-commerce platform plugins (Shopify/Woo) | Drop-in USDC checkout for major commerce platforms. | C |
| Expense management / corporate-card ops | Track, categorize, reconcile USDC card/agent spend for businesses. | C |
| Gig-worker / marketplace instant payout | Instant USDC payouts for gig and marketplace platforms. | C |
| On-chain invoicing + AR/AP | Invoice issue/track/settle in USDC with reminders + off-ramp for SMB/freelancers. | C |
| Payroll product | Multi-employee USDC payroll, scheduling, off-ramp, optional confidential amounts. | C |
| Atomic split-payments / revenue-share router | Atomic multi-party splits (your GoodDistributor pattern) for platforms/creators. | C |
| Treasury sweep / auto-rebalance automation | Rules to sweep idle USDC into yield/treasury, cross-chain. | C |
| Payment links / POS app | Merchant payment links + QR POS for in-person/online USDC. | C |
| Embeddable 'Pay with USDC' widget SDK | Drop-in button/checkout component (React/JS) wrapping App Kit + Relay. | C |
| Subscription dunning / smart-retry engine | Retry failed pull-payments and recover churn. | C |
| Payment-request / QR standard + SDK | Standardized pay-request URIs/QR for Arc USDC. | D |
| Escrow-as-a-service | Milestone/condition escrow for marketplaces/freelance. | D |
| Creator monetization / tipping rails | Tips, paid content, fan payments in USDC + nanopayments. | D |
| Donation / fundraising rails | Transparent on-chain donations with receipts. | D |

---

## Trust and Verifiability

> Tooling that makes a consortium chain safe to integrate against — monitoring, freeze protection, transparency.

| Product | What it is | Tier |
|---|---|:--:|
| Blocklist-risk + escrow protection protocol | Contract library routing a frozen address's positions into escrow instead of bricking the protocol for all users. | A |
| Dispute & validator-action monitor | Real-time alerts on tx reversals, validator rotation, blocklist/freeze events; integrator-grade. | A |
| Pre-tx screening service (OFAC/blocklist) | Non-custodial API to check addresses against blocklist/sanctions before sending. | C |
| Proof-of-reserves / attestation dashboard | Verifiable reserve/attestation display for Arc-issued tokenized assets. | C |
| Validator transparency / decentralization scoreboard | Public scoreboard tracking validator diversity, rotation, uptime, jurisdiction. | C |
| Freeze-insurance / blocklist hedging | Risk product covering USDC freeze exposure for treasuries. | D |

---

## Fiat-to-Crypto Boundary

> The fiat-to-crypto edge — the real bottleneck — with an emerging-market, Africa-first focus.

| Product | What it is | Tier |
|---|---|:--:|
| On/off-ramp aggregator + router (Africa-first) | Route across ramp providers for best rate; reuse KYC; Arc-settled. | A |
| Reusable KYC-passport across ramps | Portable verified-identity credential reused across ramps/apps. | B |
| Cash agent-network coordination layer | Coordinate human cash-in/out agents (liquidity, settlement, reputation). | B |
| Mobile-money bridge (M-Pesa/Opay/MoMo <-> USDC) | Connect mobile-money wallets to Arc USDC in/out. | B |
| Local-stablecoin issuance + Arc-bridge toolkit | Tooling to issue cNGN-class local stablecoins and bridge/list them on Arc. | B |
| Virtual-account / IBAN issuance for USDC | Issue a bank account/IBAN that settles to USDC on Arc. | C |
| Card-issuing bridge (spend USDC via card) | Issue cards that draw from an Arc USDC balance. | C |

---

## Data and Analytics

> Payments-native intelligence on top of the raw indexers that now exist but stop at generic EVM data.

| Product | What it is | Tier |
|---|---|:--:|
| Address labeling / entity resolution | Label entities, exchanges, and contracts on Arc. | C |
| Merchant / payments analytics | Revenue, settlement, and refund analytics for Arc merchants. | C |
| Stablecoin rate / yield dashboard | Compare yields and rates across Arc venues. | D |

---

## Stablecoin Issuance

> Tooling to bring new issuers, currencies, and liquidity onto Arc.

| Product | What it is | Tier |
|---|---|:--:|
| Stablecoin-issuance-as-a-service (white-label) | Launch your own compliant stablecoin on Arc — mint, redeem, reserve attestation. | A |
| Tokenized-deposit issuance for banks | Tooling for banks to issue tokenized deposits on Arc. | B |
| Yield-bearing stablecoin wrapper | Wrap USDC into a yield-bearing (USYC-backed) token with clean UX. | C |

---

## Cross-chain Infrastructure

> Orchestration that realizes Arc's settlement-hub thesis across CCTP and Gateway.

| Product | What it is | Tier |
|---|---|:--:|
| Arc-as-hub omnichain treasury rebalancer | Omnichain USDC balance manager using CCTP/Gateway. | B |
| Omnichain stablecoin SDK | One SDK to manage USDC balances/transfers across chains incl. Arc. | C |
| CCTP / bridge analytics + monitor | Monitor cross-chain USDC flows and bridge health with alerts. | C |

---

## Wallets and UX

> Embedded wallets, recovery, and policy controls tuned to Arc's USDC-gas and confidential model.

| Product | What it is | Tier |
|---|---|:--:|
| Wallet-as-a-Service (white-label embedded wallets) | Embeddable, branded self-custodial wallets for any Arc app — passkeys, recovery, gas sponsorship. | B |
| Batch-payment / mass-payout UI + SDK | CSV-to-batch USDC payouts with retries and receipts. | C |
| Treasury multisig / policy wallet | Multisig + spending policies for org treasuries — USDC-gas and confidential-aware. | C |
| Social-recovery / account-recovery module | Guardian-based recovery for Arc smart accounts. | C |
| In-wallet swap / FX widget | Embedded swap routing StableFX + AMM inside any wallet. | D |
| Address book / payment-identity contacts | Human-readable contacts wired to Payment Alias. | D |

---

## Developer Experience

> Runtime, debugging, and testing tools beyond Circle's first-party scaffolding.

| Product | What it is | Tier |
|---|---|:--:|
| TEE / confidential-transfer testing harness | Local devnet + tooling to test confidential transfers/view keys. | B |
| Arc MCP server (LLM-queryable data + actions) | MCP server exposing Arc data/actions to LLMs/agents. | B |
| ArcLens — observability + error-decoding + tx simulation SDK | Human-readable error decoding, preflight simulation, smart RPC routing for Arc. | B |
| Account-abstraction / smart-wallet SDK | Passkeys, session keys, gas-sponsorship policies on Arc. | C |
| App-level webhook / event-stream layer | Semantic webhooks on top of indexers (payment received, intent settled). | C |
| Foundry/Hardhat plugin for Arc | Blockscout verify, USDC-gas-aware gas reports, Arc presets. | C |
| Stablecoin contract-template library | Audited templates: payments, escrow, streaming, splits, subscriptions. | D |

---

## Governance and Token

> Accounting, governance, and staking tooling for ARC's still-undefined utility and the PoS transition.

| Product | What it is | Tier |
|---|---|:--:|
| ARC liquid-staking token (post-PoS) | An LST for staked ARC. | C |
| USDC-gas tax & accounting tool | Track/report USDC-as-gas for tax and books (gas-in-stablecoin is messy). | C |
| Governance/delegate dashboard + Treasury analytics | Track proposals, delegate, analyze the on-chain Arc Treasury (fees flow there). | C |
| Validator-ops / node-monitoring suite | Monitoring/alerting/ops for Arc validators. | D |
| Staking / delegation tooling (post-PoS) | Staking, delegation, rewards UX for the PoS transition. | D |
| Gas-budgeting / fee-forecasting tool | Forecast USDC fees (EIP-1559 moving-average aware) for budgeting. | D |

---

## Trade and Vertical

> Vertical settlement and financing — trade finance, factoring, marketplaces, DAOs.

| Product | What it is | Tier |
|---|---|:--:|
| Trade finance / supply-chain finance | On-chain letters of credit and PO financing settled in USDC. | B |
| B2B marketplace settlement layer | Settlement, escrow, and reconciliation for B2B marketplaces. | C |
| Invoice factoring / receivables financing | Advance against on-chain invoices. | C |
| DAO payroll / contributor payments | Streaming, batch payments, and compliance for DAOs. | C |
| Real-estate / commodities settlement | Settlement and escrow for tokenized real assets. | D |

---

## Consumer and Emerging-Market Apps

> Demand-side consumer and emerging-market apps that bring real users on-chain.

| Product | What it is | Tier |
|---|---|:--:|
| SMB neobank on Arc rails | Business accounts, payments, payroll, FX for SMBs. | C |
| Consumer USDC wallet w/ local-currency UX + ramps | Mobile wallet showing local currency, built-in ramps, Africa-first. | D |
| Savings-circle / ROSCA (esusu/ajo) dapp | Digitize rotating savings circles with USDC. | D |
| Bill-splitting / P2P consumer app | Social P2P payments + splitting in USDC. | D |
