# Audit Log Example

> **Icarus Nova** | Example audit log entries (conceptual).

## Overview

This document shows example audit log entries. This is a **conceptual example** for educational purposes.

## Example Audit Log Entries

### Invoice Created Event

```json
{
  "auditEventId": "audit-001",
  "eventType": "invoice_created",
  "timestamp": "2024-01-15T09:00:00Z",
  "organizationId": "org-12345",
  "invoiceId": "inv-67890",
  "userId": "user-abc123",
  "eventData": {
    "invoiceNumber": "001-001-000000001",
    "country": "EC"
  }
}
```

### Invoice Authorized Event

```json
{
  "auditEventId": "audit-002",
  "eventType": "invoice_authorized",
  "timestamp": "2024-01-15T10:30:00Z",
  "organizationId": "org-12345",
  "invoiceId": "inv-67890",
  "systemId": "system-xyz",
  "eventData": {
    "authorizationNumber": "1234567890",
    "authorizationDate": "2024-01-15T10:30:00Z",
    "taxAuthority": "SRI"
  }
}
```

## Related Documents

- [Audit and Traceability](../docs/audit-and-traceability.md)
- [ADR-0005: Auditability First](../adr/0005-auditability-first.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team
