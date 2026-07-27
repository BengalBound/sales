# Master SaaS Platform — Developer Infrastructure & Architecture Specification (Mobile App + Dual Web/App CEO Portal + Master SaaS Admin)

## Technical Architecture Overview
This specification defines the developer implementation details for the **Master SaaS Admin Platform, Autonomous AI Support, and Multi-Tenant Ecosystem**. 

**STRICT COMPLIANCE & TOUCHPOINT ARCHITECTURE:**
1. **Store Clerks & Salesmen:** **100% Mobile App Based** (Cross-platform **Flutter / React Native** app for Android & iOS) featuring native one-tap mic voice recording, instant camera OCR scanning, offline-first local SQLite sync, and native Mobile Money checkout (Wave, Orange Money, MTN MoMo).
2. **Subscribed Business CEOs & Store Owners (Tenants):** **DUAL ACCESS — Mobile App AND Web Dashboard Portal**. Tenant CEOs can monitor real-time sales, staff performance, inventory status, and AI support tickets from either their mobile phone app or any desktop web browser.
3. **Master Platform Admin (Us / Platform Owners):** **Web-Based Master SaaS Control Panel & IT Approval Center** (Django 5.0 + DRF + Responsive Master Admin Portal) for global network metrics, tenant billing, white-label branding, lead hunter campaigns, and Human-In-The-Loop (HITL) IT script approvals.

---

## 1. Touchpoint Architecture & Client Layer

```mermaid
graph TD
    subgraph "Tier 1: Store Clerks & Salesmen"
        ClerkApp[Android & iOS Native Mobile App - Voice & Vision]
    end

    subgraph "Tier 2: Tenant Business CEOs / Store Owners"
        CEOMobileApp[Tenant CEO Mobile App - iOS/Android Analytics]
        CEOWebPortal[Tenant CEO Web Dashboard Portal - Desktop/Browser]
    end

    subgraph "Tier 3: Master Platform Owners (Us)"
        MasterWebAdmin[Master SaaS Web Control Panel & HITL IT Approval Center]
    end

    subgraph "In-House Python Backend & Local AI Cluster"
        DjangoDRF[Python Django REST Framework APIs]
        LocalAI[Self-Hosted In-House AI Cluster: vLLM / Faster-Whisper / Qwen2-VL]
        DB[(PostgreSQL Multi-Tenant DB)]
    end

    ClerkApp -- "Voice / Vision / DRF API" --> DjangoDRF
    CEOMobileApp -- "Mobile Analytics API" --> DjangoDRF
    CEOWebPortal -- "Web Dashboard API" --> DjangoDRF
    MasterWebAdmin -- "Master SuperAdmin HTTPS" --> DjangoDRF
    DjangoDRF --> LocalAI
    DjangoDRF --> DB
```

---

## 2. Tiered Client Architecture

### 2.1 Tier 1: Store Clerks & Salesmen (100% Mobile App)
* **Native Audio & Camera Engine:** One-tap voice recording (`record` / `flutter_sound`) and instant camera OCR photo scanning (`camera` package) connected to the in-house `Qwen2-VL` vision endpoint.
* **Offline-First SQLite Caching:** Local SQLite storage caches sales entries, offline stock levels, and voice drafts. Auto-syncs with Django DRF backend when reconnected.
* **Mobile Money Payment SDKs:** One-click in-app checkout supporting Wave, Orange Money, MTN MoMo, and Moov Money.

### 2.2 Tier 2: Subscribed Tenant CEOs & Store Owners (Dual Access: Mobile App + Web Portal)
* **Real-Time Analytics Dashboard:** Real-time store revenue, daily sales charts, top-performing product rankings, inventory alerts, and salesman activity metrics.
* **Responsive Web Portal & Mobile App:** Responsive Web Portal (React / Vue / Django Templates) accessible via desktop browser AND native iOS/Android mobile dashboard app.
* **Store Management & Staff Control:** Add/remove salesman accounts, configure custom store prices, view digital receipts, and audit AI call center support transcripts.

### 2.3 Tier 3: Master SaaS Platform Admin (Us / Platform Owners)
* **Master Web Control Center:** Global real-time dashboard displaying active store counts across countries, total transaction volume, MRR, system health, and self-hosted GPU node loads.
* **White-Label Branding Engine:** Configure custom logos, colors, domain routing (`tenant.clientdomain.com`), and mobile app splash screens per enterprise customer.
* **Human-in-the-Loop (HITL) IT Approval Queue:** Web interface to review, approve, and execute AI-generated Python fix scripts for technical support tickets.
* **AI Lead Hunter Campaign Manager:** Launch and track autonomous prospecting campaigns across global target regions.

---

## 3. Autonomous 24/7 AI Call Center & IT Ticketing System

```mermaid
sequenceDiagram
    participant Merchant as Store Owner / Salesman (Mobile App / WhatsApp)
    participant PyVoiceStream as Mobile Voice Stream Bridge
    participant LocalSTT as In-House STT (Faster-Whisper)
    participant LocalLLM as In-House Multilingual LLM (Qwen2.5)
    participant LocalTTS as In-House Multilingual TTS (XTTS v2)
    participant PyTicketEngine as Python Smart Ticketing Engine
    participant MasterWebAdmin as Master Web Portal (Us / IT Admin)

    Merchant->>PyVoiceStream: One-Tap Mobile Voice / Telephony Stream
    PyVoiceStream->>LocalSTT: Transcribe Audio in Native Language
    LocalSTT-->>LocalLLM: Direct Text Stream to Local vLLM
    LocalLLM-->>LocalTTS: Generated Response Tokens -> Local TTS Engine
    LocalTTS-->>PyVoiceStream: Stream Audio Back to Mobile App / Call
    
    alt Complex Technical Issue
        PyVoiceStream->>PyTicketEngine: Auto-create Ticket + Transcribe Conversation
        PyTicketEngine->>LocalLLM: Local DeepSeek-R1 -> Generate Python Fix Script
        PyTicketEngine->>MasterWebAdmin: Push Ticket to Master Web Admin Panel (Us)
        MasterWebAdmin->>MasterWebAdmin: Platform Owner Clicks 'Approve & Execute'
    end
```

---

## 4. Universal Multi-Vendor Inventory & Ecosystem

### 4.1 Mobile App & Web Portal Inventory Management
* **Catalog Browsing:** Fast scrolling list view on mobile app and tabular grid view on CEO web portal with instant voice search and camera photo matching.
* **Dynamic Form Rendering:** Mobile app and Web portal dynamically render input fields based on JSON schemas received from Django DRF endpoints (`attributes` JSONB column).
