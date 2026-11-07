# Autonomous Data-Gated Stablecoin Escrow Gateway
> **Cleva × Tether Future of Payments Hackathon Submission (UNIUYO Edition)**

---

## 📌 Project Overview
This project introduces an **Intelligent, Data-Driven Smart Escrow Payment Engine** engineered to solve cross-border settlement bottlenecks in underbanked markets. By combining **Tether (USDT)** on-chain liquidity with **Cleva’s** seamless local fiat (NGN) off-ramp infrastructure, the platform replaces static financial channels with automated, risk-aware payment releases.

While domain-agnostic across B2B freelancer payroll, e-commerce, and logistics, our prototype demonstrates real-world economic utility through **agricultural export supply chain settlements**. It ingests telemetry data, runs a machine learning predictive model to evaluate crop spoilage risk, and programmatically releases USDT into local Naira directly to a vendor’s bank account upon verification.

---

## ⚙️ Key Architectural Features

- **Tether (USDT) Liquidity Engine:** Bypasses international wire transfer delays (3–5 days) and cuts cross-border settlement fees by up to 80%.
- **Cleva Off-Ramp Integration:** Automatically converts released stablecoins directly into spendable local Naira (NGN) into the vendor's bank account with zero crypto friction for the recipient.
- **Predictive Risk Modeling:** Evaluates transit metrics (transit hours, ambient temperature, humidity) using a Decision Tree Classifier trained in Google Colab to protect both buyer and seller from counterparty default.
- **Low-Code Visual Automation:** Built on an **n8n** visual pipeline (self-hostable via Docker) to manage webhooks, ML logic execution, API routing, and notification dispatching.
- **Instant Messaging Alerts:** Dispatches real-time, zero-cost transaction notifications directly to rural vendors via Telegram API.

---

## 🏗 System Architecture Flow

```text
[ International Buyer ]
           │
  Deposits USDT Escrow
           │
           ▼
[ Shipment Sensor / Telemetry Log ] ──(POST Webhook Payload)──► [ n8n Automation Engine ]
                                                                        │
                                                                        ▼
                                                           [ Python ML Decision Node ]
                                                             (Evaluates Spoilage Risk)
                                                                        │
                                                      ┌─────────────────┴─────────────────┐
                                              Risk = LOW                         Risk = HIGH
                                                      │                                   │
                                                      ▼                                   ▼
                                           [ Execute Cleva Off-Ramp ]            [ Lock Smart Escrow ]
                                           (Converts USDT ➔ NGN Bank Deposit)      (Trigger Alert for Review)
                                                      │                                   │
                                                      ▼                                   ▼
                                            [ Telegram Vendor Alert ]           [ Telegram Risk Alert ]