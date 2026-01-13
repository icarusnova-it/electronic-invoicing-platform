# Tax Authority Adapters

> **Icarus Nova** | Architecture and implementation of tax authority adapters.

## Overview

Tax authority adapters implement country-specific integration logic while maintaining a common interface with the core platform.

## Adapter Interface

### Common Methods

- `submitInvoice(invoice)`: Submit invoice to tax authority
- `checkAuthorization(submissionId)`: Check authorization status
- `getAuthorizationDetails(authorizationId)`: Get authorization details
- `validateInvoice(invoice)`: Country-specific validation

## Country Adapters

### SRI Adapter (Ecuador)

**Integration:**
- SOAP web services
- Certificate-based authentication
- Asynchronous authorization

### SUNAT Adapter (Peru)

**Integration:**
- SOAP web services
- Certificate-based authentication
- Asynchronous authorization

### DIAN Adapter (Colombia)

**Integration:**
- SOAP web services
- Certificate-based authentication
- Asynchronous authorization

## Related Documents

- [Tax Authority Integration](../diagrams/tax-authority-integration.md)
- [ADR-0001: Regulator-Agnostic Design](../adr/0001-regulator-agnostic-design.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team  
**Version:** 1.0
