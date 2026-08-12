# BOUND OS — 3-Month Execution Roadmap (Dual App/Web CEO Portal + Mobile Clerk App)

## Overview
This 3-Month Execution Plan organizes development into iterative 30-day sprints for **BOUND OS** ("Country first. Software second."). Each phase delivers fully audited, production-ready modules, scaling up from the current live footprint (**1,214 stores across Côte d'Ivoire, Senegal, and Bangladesh generating $84.3k MRR**) to global pipeline expansion markets (Ethiopia, Nigeria, Nepal, India, Pakistan, Sri Lanka), powered by our **Active Primary Production Cloud API Stack (~$1,269/mo)**.

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
| MONTH 2: CLOUD API VOICE/VISION INTEGRATION, CALL CENTER & HITL IT TICKETING      |
| - Deepgram Nova-2 STT ($645/mo) + Gemini 1.5 Flash LLM ($76/mo) Pipeline           |
| - Azure Standard TTS ($480/mo) + Gemini Multimodal Vision Integration             |
| - Smart Ticketing Engine & 1-Click IT Script Execution ($ approve --ticket ...)   |
+-----------------------------------------------------------------------------------+
                                        |
                                        v
+-----------------------------------------------------------------------------------+
| MONTH 3: WHITE-LABEL ENGINE, HETZNER CLOUD VPS HARDENING & GLOBAL SCALING         |
| - White-Label Theme Customization Engine (Mobile Splash + Domain Routing)        |
| - Production Hetzner Cloud CPX VPS & Managed PostgreSQL Topology (~$65/mo)       |
| - Merchant Onboarding in 6 Expansion Pipeline Markets (ET, NG, NP, IN, PK, LK)   |
+-----------------------------------------------------------------------------------+
```

---

## Month 1: Core Multi-Tenant Engine & App/Web Touchpoints

### Sprint 1.1 (Days 1 - 15): Master Admin & Tenant CEO Dual Portals
* **Tasks:**
  - Setup Django 5.0 project structure with tenant isolation middleware (`TenantScopedModel`).
  - Build Master SaaS Web Control Panel for platform owners: Global Active Stores (1,214 current), System Health, Total Revenue ($84.3k MRR), Registered Users (3,642), API cost load cards ($1,269/mo primary).
  - Build Tenant CEO Dashboard views accessible via both **Desktop Web Browser** and **Mobile App** with role-based permission keys (`accView`, `accApprove`, `accPrice`, `accTeam`, `accExport`).
  - **Client Milestone:** Confirm Primary Production Cloud API Stack (~$1,269/mo) and secondary self-hosted GPU toggle options.
* **Deliverables:** Operational Master Admin web portal + Tenant CEO dual Web/App portal + Production Stack Sign-Off.

### Sprint 1.2 (Days 16 - 30): Mobile Clerk App & Multilingual Vision OCR Engine
* **Tasks:**
  - Build Flutter Mobile App for Store Clerks & Salesmen (`rep` role) with 96px minimum touch targets for 2-tap sales flow.
  - Integrate Deepgram Nova-2 STT streaming and Gemini 1.5 Flash Multimodal OCR camera scanner (`docDelivery`, `docInvoice`, `docCard`).
  - Implement offline SQLite caching and auto-sync replay queue with deduplicating idempotency keys.
* **Deliverables:** Native Mobile Clerk App with one-tap voice & camera stock updates.

---

## Month 2: Multilingual AI Engine, Dialect Adaptation & HITL Ticketing

### Sprint 2.1 (Days 31 - 45): Autonomous AI Call Center & Cloud Voice Pipeline
* **Tasks:**
  - Configure Deepgram Nova-2 STT and Gemini 1.5 Flash LLM for West African and South Asian regional trade dialects (**Nouchi street slang**, **Dioula**, **Wolof**, **Pulaar**, **Sylheti**, **Chittagonian**).
  - Integrate Azure Standard TTS ($480/mo) for real-time speech synthesis in 100+ native languages.
  - Implement WebRTC / SIP telephony stream handler (`record` package & DRF voice endpoints).
* **Deliverables:** Operational 24/7 AI Call Center natively processing regional trade dialects via Cloud APIs at $1,269/mo baseline.

### Sprint 2.2 (Days 46 - 60): Multilingual Lead Hunter & HITL IT Ticketing Sandbox
* **Tasks:**
  - Build autonomous Lead Hunter prospecting engine (Python scraper + Gemini 1.5 Flash).
  - Implement Smart IT Ticketing Queue and Master Admin 1-Click Code Approval web sandbox (`$ approve --ticket 4127 --execute`).
* **Deliverables:** Fully working Lead Hunter campaign system & HITL IT ticket approval queue.

---

## Month 3: White-Label Engine, Hardware Topology & Commercial Rollout

### Sprint 3.1 (Days 61 - 75): Production Hetzner Cloud Topology & Infrastructure Hardening
* **Tasks:**
  - Deploy production Hetzner Cloud CPX VPS + Managed PostgreSQL database topology at **~$65/mo flat cost**.
  - Route Deepgram Nova-2 ($645/mo), Gemini 1.5 Flash ($76/mo), and Azure TTS ($480/mo) streaming WebSockets into unified high-availability environment.
  - Audit financial metrics (97.2% gross margin at $84.3k MRR current scale).
* **Deliverables:** Production-hardened $1,269/mo Cloud API infrastructure serving all AI models & web services.

### Sprint 3.2 (Days 76 - 90): Global Pipeline Merchant Rollout
* **Tasks:**
  - Expand merchant onboarding from active hubs (Abidjan Adjamé, Dakar Sandaga, Dhaka Karwan Bazar) into 6 pipeline expansion markets: **Ethiopia** (Addis Ababa), **Nigeria** (Lagos), **Nepal** (Kathmandu), **India** (Delhi NCR), **Pakistan** (Karachi), and **Sri Lanka** (Colombo).
  - Integrate native mobile payment SDKs (Telebirr, OPay, eSewa, UPI, JazzCash, LankaPay).
* **Deliverables:** Multi-region global platform rollout with audited 97.2% gross margins.


