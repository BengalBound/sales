# Master SaaS Platform — Universal Data Schemas & API Specification (Mobile App + Dual CEO Web/App Portal)

## Overview
This document specifies the core Python database schemas (Django ORM), JSON Pydantic schemas, and REST API definitions (Django REST Framework) for developers implementing the 100% in-house self-hosted AI ecosystem supporting **Mobile Clerk Apps, Dual Web/Mobile CEO Portals, and Master Admin Web Control**.

---

## 1. Core Python Database Schemas (`models.py`)

### 1.1 Universal Inventory Schema (`models.py`)
```python
from django.db import models
from django.db.models import JSONField

class TenantScopedModel(models.Model):
    """
    Abstract Python Django Base Model for automatic multi-tenant data isolation.
    """
    tenant = models.ForeignKey('accounts.BusinessInstance', on_delete=models.CASCADE, related_name="%(class)ss")
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True

class UniversalInventoryItem(TenantScopedModel):
    """
    Universal Multi-Vendor Inventory Schema in Python Django ORM.
    Supports standard SQL columns alongside dynamic EAV JSONB attributes in any language.
    """
    sku = models.CharField(max_length=64, db_index=True)
    name = models.CharField(max_length=255)
    category = models.CharField(max_length=100, db_index=True)
    price = models.DecimalField(max_digits=12, decimal_places=2)
    cost_price = models.DecimalField(max_digits=12, decimal_places=2, null=True, blank=True)
    stock_quantity = models.DecimalField(max_digits=10, decimal_places=2, default=0)
    unit = models.CharField(max_length=20, default="unit") # e.g. kg, pcs, box
    
    # Vision & OCR matching keywords across 80+ written scripts
    vision_keywords = JSONField(default=list, help_text="OCR text tokens for visual camera matching in native scripts")
    
    # EAV Dynamic Attributes per merchant type & region
    attributes = JSONField(default=dict, help_text="Flexible key-value pairs (e.g. color, size, expiry_date, supplier_code)")
    
    is_active = models.BooleanField(default=True)

    class Meta:
        unique_together = ('tenant', 'sku')
```

### 1.2 Tenant White-Label Branding Schema (`models.py`)
```python
class TenantBranding(models.Model):
    """
    Python Django Tenant Branding Model for dynamic white-label theme injection across Web Portal & Mobile App.
    """
    tenant = models.OneToOneField('accounts.BusinessInstance', on_delete=models.CASCADE, related_name="branding")
    company_name = models.CharField(max_length=128)
    custom_domain = models.CharField(max_length=255, unique=True, null=True, blank=True)
    logo_url = models.URLField(blank=True)
    mobile_splash_url = models.URLField(blank=True, help_text="Custom splash image for Tenant CEO & Clerk Mobile App")
    primary_color = models.CharField(max_length=7, default="#4F46E5") # Hex code
    secondary_color = models.CharField(max_length=7, default="#10B981")
    font_family = models.CharField(max_length=64, default="Inter")
    custom_css = models.TextField(blank=True)
    native_language = models.CharField(max_length=10, default="fr", help_text="ISO language/dialect code (e.g. fr, nouchi, dioula, bn, hi, es, ar)")
```

---

## 2. Python REST API Endpoints Specification (Django REST Framework)

| Method | Endpoint Route | View / Handler (Python DRF) | Client Touchpoint Target | Multilingual & Dialect Capability | Access Control |
|--------|----------------|----------------------------|--------------------------|-----------------------------------|----------------|
| `GET` | `/api/v1/master/overview/` | `MasterMetricsView.as_view()` | **Master Web Portal (Us)** | Global Region Metrics & GPU Load | Master SuperAdmin |
| `GET` | `/api/v1/ceo/dashboard-analytics/` | `CEODashboardView.as_view()` | **Tenant CEO Mobile App & Web Portal** | Native Language & Dialects | Tenant CEO / Admin |
| `GET/POST` | `/api/v1/inventory/items/` | `UniversalInventoryViewSet` | **Mobile App & Web Portal** | Multilingual Product Attributes | Tenant Authenticated |
| `POST` | `/api/v1/vision/ocr-match/` | `VisionOCRMatchView.as_view()` | **Clerk Mobile App (Camera Scan)** | **80+ Written Scripts (Included in Flat Rate)** | Tenant Salesman |
| `POST` | `/api/v1/voice/telephony-webhook/` | `VoiceTelephonyBridgeView.as_view()` | **Mobile App (Mic) & Telephony** | **99+ Spoken Languages & Dialects (Nouchi, Dioula)** | Telephony Signature |
| `GET/POST` | `/api/v1/support/tickets/` | `ITSupportTicketViewSet` | **Mobile App & CEO Web Portal** | Native Language Support Tickets | Tenant User / AI Agent |
| `POST` | `/api/v1/support/tickets/{id}/approve/` | `ApproveAndExecuteScriptView.as_view()` | **Master Web Portal (Us)** | Dynamic Code Execution | IT Admin Only |
| `GET/POST` | `/api/v1/lead-hunter/campaigns/` | `LeadHunterCampaignViewSet` | **Master Web Portal (Us)** | **Global Pitch Generation** | Master Admin / Enterprise |

> **Architecture Routing Adapter Note:** Django REST Framework handlers (`VoiceTelephonyBridgeView` & `VisionOCRMatchView`) support dynamic routing backends:
> - **Option 1 & 2 (In-House vLLM):** Routes audio/image payloads directly to local `vLLM` & `Faster-Whisper` socket endpoints ($0.00 variable fee).
> - **Option 3 & 4 (3rd-Party APIs):** Routes audio/image payloads to Groq Turbo / Gemini 2.0 / Deepgram API gateways via environment flags (`AI_ENGINE_BACKEND=vllm|groq|gemini`).
