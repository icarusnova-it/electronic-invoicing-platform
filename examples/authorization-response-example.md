# Authorization Response Example

> **Icarus Nova** | Example authorization response from tax authority (conceptual).

## Overview

This document shows an example authorization response structure. This is a **conceptual example** for educational purposes.

## Example Authorization Response

### Success Response

```json
{
  "authorizationId": "auth-12345",
  "invoiceId": "inv-67890",
  "authorizationNumber": "1234567890",
  "authorizationDate": "2024-01-15T10:30:00Z",
  "status": "authorized",
  "taxAuthority": "SRI",
  "submissionId": "sub-001"
}
```

### Rejection Response

```json
{
  "authorizationId": "auth-12346",
  "invoiceId": "inv-67891",
  "status": "rejected",
  "taxAuthority": "SRI",
  "errorCode": "ERR-001",
  "errorMessage": "Invalid tax ID",
  "submissionId": "sub-002"
}
```

## Related Documents

- [Invoice Lifecycle](../docs/invoice-lifecycle.md)
- [ADR-0003: Asynchronous Authorization](../adr/0003-asynchronous-authorization.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team
