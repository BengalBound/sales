# Master SaaS Platform — 3-Month Execution Roadmap (Dual App/Web CEO Portal + Mobile Clerk App)

## Overview
This 3-Month Execution Plan organizes development into iterative 30-day sprints. Each phase delivers fully audited, production-ready modules, building up to the commercial rollout of the global multi-tenant platform powered by our **100% in-house self-hosted AI engine supporting mobile app clients, dual CEO portals, and master web admin control**.

---

## Roadmap Timeline Summary

```
+-----------------------------------------------------------------------------------+
| MONTH 1: CORE MULTI-TENANT ENGINE, MOBILE CLERK APP & DUAL CEO DASHBOARD          |
| - Master SaaS Web Control Panel & Tenant Isolation Middleware                       |
| - Flutter Mobile App Scaffold for Clerks (Voice & Camera OCR Engine)              |
| - Tenant CEO Dual Dashboard (Mobile App + Desktop Web Portal)                     |
+-----------------------------------------------------------------------------------+
                                        |
                                        v
+-----------------------------------------------------------------------------------+
| MONTH 2: MULTILINGUAL LEAD HUNTER, VOICE CALL CENTER & HITL TICKETING              |
| - Autonomous Lead Hunter Engine (Python Scraper + Multilingual DeepSeek-R1)        |
| - 24/7 Voice AI Call Center (Local Faster-Whisper 99+ Langs + XTTS v2 + Qwen2.5)  |
| - Smart Ticketing Engine & Human-in-the-Loop (HITL) IT Script Approval Web Panel   |
+-----------------------------------------------------------------------------------+
                                        |
                                        v
+-----------------------------------------------------------------------------------+
| MONTH 3: WHITE-LABEL ENGINE, HARDENING, GPU SERVING & GLOBAL PILOT ROLLOUT         |
| - White-Label Theme Customization Engine (Mobile App Splash + Web Domain/CSS)     |
| - Production Hetzner GPU Dedicated Topology (AX102 Multilingual vLLM Cluster)     |
| - Global Pilot Merchant Onboarding (50 Test Stores) & Commercial Launch           |
+-----------------------------------------------------------------------------------+
```

---

## Month 1: Core Multi-Tenant Engine & App/Web Touchpoints

### Sprint 1.1 (Days 1 - 15): Master Admin & Tenant CEO Dual Portals
* **Tasks:**
  - Setup Django 5.0 project structure with tenant isolation middleware (`TenantScopedModel`).
  - Build Master SaaS Web Control Panel for platform owners (Us): Global Active Stores, System Health, Total Revenue, Registered Users, GPU load cards.
  - Build Tenant CEO Dashboard views accessible via both **Desktop Web Browser** and **Mobile App**.
  - **Client Milestone:** Present Client Architecture Selection Matrix (Option 1: $99/mo Single-Node vs Option 2: $194.50/mo Multi-Node vs Option 3: $314.67/mo API Bridge) for final client sign-off.
* **Deliverables:** Operational Master Admin web portal + Tenant CEO dual Web/App portal + Client Architecture Selection Sign-Off.

### Sprint 1.2 (Days 16 - 30): Mobile Clerk App & Multilingual Vision OCR Engine
* **Tasks:**
  - Build Flutter Mobile App for Store Clerks & Salesmen (Android & iOS).
  - Integrate native voice audio recording and camera photo scanner (`Qwen2-VL-7B` / `PaddleOCR` endpoint).
  - Implement offline SQLite caching and auto-sync with Django DRF endpoints.
* **Deliverables:** Native Mobile Clerk App with one-tap voice & camera stock updates.

---

## Month 2: Multilingual AI Engine, Dialect Adaptation & HITL Ticketing

### Sprint 2.1 (Days 31 - 45): Autonomous AI Call Center & Regional Dialect Tuning
* **Tasks:**
  - Fine-tune `Faster-Whisper` STT and `Qwen2.5-7B` LLM for West African regional dialects (**Nouchi street slang** & **Dioula trade language**) alongside 99+ global languages.
  - Deploy `Coqui XTTS v2` voice cloning engine with real-time zero-cost speech synthesis.
  - Implement WebRTC / SIP telephony stream handler (`record` package & DRF voice endpoints).
* **Deliverables:** Operational 24/7 AI Call Center natively processing Nouchi, Dioula, French, and global languages with zero variable API fees.

### Sprint 2.2 (Days 46 - 60): Multilingual Lead Hunter & HITL IT Ticketing Sandbox
* **Tasks:**
  - Build autonomous Lead Hunter prospecting engine (Python scraper + `DeepSeek-R1-Distill-Qwen-14B`).
  - Implement Smart IT Ticketing Queue and Master Admin 1-Click Code Approval web sandbox (`ApproveAndExecuteScriptView`).
* **Deliverables:** Fully working Lead Hunter campaign system & HITL IT ticket approval queue.

---

## Month 3: White-Label Engine, Hardware Topology & Commercial Rollout

### Sprint 3.1 (Days 61 - 75): Production GPU Cluster & Dedicated Server Synergy
* **Tasks:**
  - Deploy production Hetzner Dedicated GPU topology: **AX102** (AMD Ryzen 9 7950X / RTX 4090 24GB VRAM) + **CPX31** node at **$194.50/mo flat cost**.
  - Consolidate AI inference (`vLLM`), core Django APIs, PostgreSQL multi-tenant database, and Redis broker into single high-performance environment.
  - Validate financial margins (99.3% gross profit, $1,074.50/mo net profit saved vs 3rd-party API stack at 1,000 stores).
* **Deliverables:** Production-hardened $194.50/mo flat rate infrastructure serving all AI models & web services.

### Sprint 3.2 (Days 76 - 90): Global Pilot Merchant Rollout (Ivory Coast & Beyond)
* **Tasks:**
  - Onboard 50 pilot merchants across Abidjan (Adjamé, Treichville, Cocody) using Wave Mobile Money and WhatsApp voice note integration.
  - Audit system latency (< 250ms STT, < 200ms LLM), voice recognition accuracy on Nouchi/Dioula, and zero-token-anxiety stability.
* **Deliverables:** Commercial platform launch with audited 99.3% gross margins.
