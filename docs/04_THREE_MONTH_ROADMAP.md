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
* **Deliverables:** Operational Master Admin web portal + Tenant CEO dual Web/App portal.

### Sprint 1.2 (Days 16 - 30): Mobile Clerk App & Multilingual Vision OCR Engine
* **Tasks:**
  - Build Flutter Mobile App for Store Clerks & Salesmen (Android & iOS).
  - Integrate native voice audio recording and camera photo scanner (`Qwen2-VL-7B` / `PaddleOCR` endpoint).
  - Implement offline SQLite caching and auto-sync with Django DRF endpoints.
* **Deliverables:** Native Mobile Clerk App with one-tap voice & camera stock updates.
