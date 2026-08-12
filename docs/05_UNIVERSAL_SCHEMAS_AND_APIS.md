# BOUND OS — Universal Data Schemas & API Specification

## Overview
This document specifies the core Python database schemas (Django ORM), JSON Pydantic schemas, and REST API definitions (Django REST Framework) for developers implementing **BOUND OS** ("Country first. Software second.").

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
    country = models.CharField(max_length=5, db_index=True, help_text="ISO Country Code driving dynamic region logic (CI, SN, BD, ET, NG, etc.)")
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
    cost_price = models.DecimalField(max_digits=12, decimal_places=2)
    price = models.DecimalField(max_digits=12, decimal_places=2)
    commission_rate = models.DecimalField(max_digits=5, decimal_places=2, default=5.0) # e.g. 5%
    stock_quantity = models.DecimalField(max_digits=10, decimal_places=2, default=0)
    unit = models.CharField(max_length=20, default="unit") # e.g. kg, pcs, set, box
    
    # Vision & OCR matching keywords across 80+ written scripts
    vision_keywords = JSONField(default=list, help_text="OCR text tokens for visual camera matching in native scripts")
    
    # EAV Dynamic Attributes per merchant type & region
    attributes = JSONField(default=dict, help_text="Flexible key-value pairs (e.g. color, size, expiry_date, supplier_code)")
    
    is_active = models.BooleanField(default=True)

    class Meta:
        unique_together = ('tenant', 'sku')
```

### 1.2 User Roles & Granular Permission Schema (`models.py`)
```python
class UserPermissionProfile(models.Model):
    """
    User Permission Schema enforcing 3-Tier Access Control across Mobile App & Web Portal.
    """
    ROLE_CHOICES = [
        ('rep', 'Store Clerk / Sales Rep'),
        ('manager', 'Store Manager'),
        ('owner', 'Business Owner'),
    ]
    
    user = models.OneToOneField('auth.User', on_delete=models.CASCADE, related_name="permission_profile")
    role = models.CharField(max_length=20, choices=ROLE_CHOICES, default='rep')
    
    # Granular Override Permissions (JSON map)
    # Keys: accView, accApprove, accPrice, accTeam, accExport
    custom_permissions = JSONField(default=dict, blank=True, help_text="Explicit boolean overrides for PERM_KEYS")

    def has_permission(self, perm_key: str) -> bool:
        if perm_key in self.custom_permissions:
            return self.custom_permissions[perm_key]
        DEFAULT_ROLE_PERMS = {
            'rep': ['accView'],
            'manager': ['accView', 'accApprove', 'accExport'],
            'owner': ['accView', 'accApprove', 'accPrice', 'accTeam', 'accExport']
        }
        return perm_key in DEFAULT_ROLE_PERMS.get(self.role, [])
```

### 1.3 Task Assignment & Micro-Messaging Schema (`models.py`)
```python
class StoreTask(TenantScopedModel):
    """
    Task Assignment Schema supporting Scope-Based Direct Routing (CAN_SEND rules).
    """
    PRIORITY_CHOICES = [('low', 'Low'), ('normal', 'Normal'), ('urgent', 'Urgent')]
    STATUS_CHOICES = [('todo', 'To Do'), ('half', 'In Progress'), ('done', 'Done')]
    
    sender = models.ForeignKey('auth.User', on_delete=models.CASCADE, related_name="sent_tasks")
    recipient_role = models.CharField(max_length=20) # 'rep', 'manager', or 'owner'
    label = models.CharField(max_length=255)
    description = models.TextField(blank=True)
    priority = models.CharField(max_length=10, choices=PRIORITY_CHOICES, default='normal')
    status = models.CharField(max_length=10, choices=STATUS_CHOICES, default='todo')
    ai_drafted = models.BooleanField(default=False)
```

---

## 2. Python REST API Endpoints Specification (Django REST Framework)

| Method | Endpoint Route | View / Handler (Python DRF) | Client Touchpoint Target | Multilingual & Dialect Capability | Access Control |
|--------|----------------|----------------------------|--------------------------|-----------------------------------|----------------|
| `GET` | `/api/v1/master/overview/` | `MasterMetricsView.as_view()` | **Master Web Portal** | Global Network Metrics & GPU Load | Master Admin Only |
| `GET` | `/api/v1/ceo/dashboard-analytics/` | `CEODashboardView.as_view()` | **Tenant CEO Mobile & Web Portal** | Native Language & Dialects | `accView` |
| `GET/POST` | `/api/v1/inventory/items/` | `UniversalInventoryViewSet` | **Mobile App & Web Portal** | Multilingual Product Attributes | `accView` / `accPrice` |
| `POST` | `/api/v1/vision/ocr-match/` | `VisionOCRMatchView.as_view()` | **Clerk Mobile App (Camera Scan)** | **`delivery`, `invoice`, `card` OCR processing** | `accView` |
| `POST` | `/api/v1/voice/telephony-webhook/` | `VoiceTelephonyBridgeView.as_view()` | **Mobile App (Mic) & Voice Call** | **99+ Spoken Languages (212ms STT / 187ms LLM)** | Tenant Authenticated |
| `POST` | `/api/v1/offline/sync-queue/` | `OfflineQueueReplayView.as_view()` | **Clerk Mobile App (Background Sync)** | **Idempotent Queue Deduplication** | Tenant Authenticated |
| `GET/POST` | `/api/v1/tasks/` | `StoreTaskViewSet` | **Mobile App & CEO Web Portal** | Scope-restricted task delegation (`CAN_SEND`) | Tenant Authenticated |
| `GET/POST` | `/api/v1/support/tickets/` | `ITSupportTicketViewSet` | **Mobile App & CEO Web Portal** | Support Tickets & Conversation Logs | Tenant User / AI Agent |
| `POST` | `/api/v1/support/tickets/{id}/approve/` | `ApproveAndExecuteScriptView.as_view()` | **Master Web Portal** | **1-Click IT Code Execution** (`$ approve --ticket ...`) | Platform Owner Only |

> **Architecture Routing Adapter Note:** Django REST Framework handlers (`VoiceTelephonyBridgeView` & `VisionOCRMatchView`) support dynamic routing backends:
> - **Option 1 & 2 (In-House vLLM):** Routes audio/image payloads directly to local `vLLM` & `Faster-Whisper` socket endpoints ($0.00 variable fee).
> - **Option 3 & 4 (3rd-Party APIs):** Routes audio/image payloads to Groq Turbo / Gemini 2.0 / Deepgram API gateways via environment flags (`AI_ENGINE_BACKEND=vllm|groq|gemini`).

