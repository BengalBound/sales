# BOUND OS — 3-Month Execution Roadmap (Dual App/Web CEO Portal + Mobile Clerk App)

## Overview
This 3-Month Execution Plan organizes development into iterative 30-day sprints for **BOUND OS** ("Country first. Software second."). Each phase delivers fully audited, production-ready modules, scaling up from the current live footprint (**1,214 stores across Côte d'Ivoire, Senegal, and Bangladesh generating $84.3k MRR**) to global pipeline expansion markets (Ethiopia, Nigeria, Nepal, India, Pakistan, Sri Lanka).

---

## Roadmap Timeline Summary

```
+-----------------------------------------------------------------------------------+
| MONTH 1: CORE MULTI-TENANT ENGINE, DYNAMIC REGION DRIVER & CLERK MOBILE APP        |
| - Master SaaS Web Control Panel & JWT Country Token Resolution Middleware         |
| - Single Flutter Mobile App Codebase for Clerks (Voice & Camera OCR Engine)       |
| - Tenant Manager & Owner Dual Dashboard (Mobile App + Desktop Web Portal)         |
+-----------------------------------------------------------------------------------+
                                        |
                                        v
+-----------------------------------------------------------------------------------+
| MONTH 2: MULTILINGUAL DIALECT TUNING, VOICE CALL CENTER & HITL IT TICKETING       |
| - Autonomous Lead Hunter Engine (Python Scraper + Multilingual DeepSeek-R1)       |
| - 24/7 Voice AI Call Center (Faster-Whisper STT 212ms + XTTS v2 + Qwen2.5 187ms)  |
| - Smart Ticketing Engine & 1-Click IT Script Execution ($ approve --ticket ...)   |
+-----------------------------------------------------------------------------------+
                                        |
                                        v
+-----------------------------------------------------------------------------------+
| MONTH 3: WHITE-LABEL ENGINE, GPU INFRASTRUCTURE HARDENING & GLOBAL SCALING        |
| - White-Label Theme Customization Engine (Mobile Splash + Domain Routing)        |
| - Production Hetzner GPU Dedicated Topology (AX102 + CPX31 @ $194.50/mo flat)     |
| - Merchant Onboarding in 6 Expansion Pipeline Markets (ET, NG, NP, IN, PK, LK)   |
+-----------------------------------------------------------------------------------+
```

---

## Month 1: Core Multi-Tenant Engine & App/Web Touchpoints

### Sprint 1.1 (Days 1 - 15): Master Admin & Tenant CEO Dual Portals
* **Tasks:**
  - Setup Django 5.0 project structure with tenant isolation middleware (`TenantScopedModel`).
  - Build Master SaaS Web Control Panel for platform owners: Global Active Stores (1,214 current), System Health, Total Revenue ($84.3k MRR), Registered Users (3,642), GPU load cards.
  - Build Tenant CEO Dashboard views accessible via both **Desktop Web Browser** and **Mobile App** with role-based permission keys (`accView`, `accApprove`, `accPrice`, `accTeam`, `accExport`).
  - **Client Milestone:** Present Client Architecture Selection Matrix (Option 1: $99/mo Single-Node vs Option 2: $194.50/mo Multi-Node vs Option 3: $314.67/mo API Bridge) for final client sign-off.
* **Deliverables:** Operational Master Admin web portal + Tenant CEO dual Web/App portal + Client Architecture Selection Sign-Off.

### Sprint 1.2 (Days 16 - 30): Mobile Clerk App & Multilingual Vision OCR Engine
* **Tasks:**
  - Build Flutter Mobile App for Store Clerks & Salesmen (`rep` role) with 96px minimum touch targets for 2-tap sales flow.
  - Integrate native voice audio recording and camera photo document scanner (`docDelivery`, `docInvoice`, `docCard` → `actStockIn`, `actPriceCheck`, `actRecordSale`, `actSaveContact`, `actAddSupplier`).
  - Implement offline SQLite caching and auto-sync replay queue with deduplicating idempotency keys.
* **Deliverables:** Native Mobile Clerk App with one-tap voice & camera stock updates.

---

## Month 2: Multilingual AI Engine, Dialect Adaptation & HITL Ticketing

### Sprint 2.1 (Days 31 - 45): Autonomous AI Call Center & Regional Dialect Tuning
* **Tasks:**
  - Fine-tune `Faster-Whisper` STT and `Qwen2.5-7B` LLM for West African and South Asian regional trade dialects (**Nouchi street slang**, **Dioula**, **Wolof**, **Pulaar**, **Sylheti**, **Chittagonian**).
  - Deploy `Coqui XTTS v2` voice cloning engine with real-time zero-cost speech synthesis (< 180ms TTS).
  - Implement WebRTC / SIP telephony stream handler (`record` package & DRF voice endpoints).
* **Deliverables:** Operational 24/7 AI Call Center natively processing regional trade dialects with 212ms STT and 187ms LLM latency at $0.00 variable API cost.

### Sprint 2.2 (Days 46 - 60): Multilingual Lead Hunter & HITL IT Ticketing Sandbox
* **Tasks:**
  - Build autonomous Lead Hunter prospecting engine (Python scraper + `DeepSeek-R1-Distill-Qwen-14B`).
  - Implement Smart IT Ticketing Queue and Master Admin 1-Click Code Approval web sandbox (`$ approve --ticket 4127 --execute`).
* **Deliverables:** Fully working Lead Hunter campaign system & HITL IT ticket approval queue.

---

## Month 3: White-Label Engine, Hardware Topology & Commercial Rollout

### Sprint 3.1 (Days 61 - 75): Production GPU Cluster & Dedicated Server Synergy
* **Tasks:**
  - Deploy production Hetzner Dedicated GPU topology: **AX102** (AMD Ryzen 9 7950X / RTX 4090 24GB VRAM) + **CPX31** node at **$194.50/mo flat cost**.
  - Consolidate AI inference (`vLLM`), core Django APIs, PostgreSQL multi-tenant database, and Redis broker into single high-performance environment.
  - Validate financial margins (99.3%+ gross profit, $1,074.50/mo net profit saved vs 3rd-party API stack at 1,000 stores).
* **Deliverables:** Production-hardened $194.50/mo flat rate infrastructure serving all AI models & web services.

### Sprint 3.2 (Days 76 - 90): Global Pipeline Merchant Rollout
* **Tasks:**
  - Expand merchant onboarding from active hubs (Abidjan Adjamé, Dakar Sandaga, Dhaka Karwan Bazar) into 6 pipeline expansion markets: **Ethiopia** (Addis Ababa), **Nigeria** (Lagos), **Nepal** (Kathmandu), **India** (Delhi NCR), **Pakistan** (Karachi), and **Sri Lanka** (Colombo).
  - Integrate native mobile payment SDKs (Telebirr, OPay, eSewa, UPI, JazzCash, LankaPay).
* **Deliverables:** Multi-region global platform rollout with audited 99.3%+ gross margins.

