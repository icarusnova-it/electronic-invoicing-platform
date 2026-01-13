# Tax Authority Integration Diagram

> **Icarus Nova** | Integration patterns with tax authorities across different countries.

## Overview

This diagram shows how the platform integrates with different tax authorities using the adapter pattern.

## Integration Architecture

```mermaid
graph TB
    subgraph "Core Platform"
        Core[Core Services]
        AdapterInterface[Adapter Interface]
    end
    
    subgraph "Country Adapters"
        SRI[SRI Adapter<br/>Ecuador]
        SUNAT[SUNAT Adapter<br/>Peru]
        DIAN[DIAN Adapter<br/>Colombia]
        SAT[SAT Adapter<br/>Mexico]
    end
    
    subgraph "Tax Authorities"
        SRI_WS[SRI Web Service]
        SUNAT_WS[SUNAT Web Service]
        DIAN_WS[DIAN Web Service]
        SAT_WS[SAT Web Service]
    end
    
    Core --> AdapterInterface
    AdapterInterface --> SRI
    AdapterInterface --> SUNAT
    AdapterInterface --> DIAN
    AdapterInterface --> SAT
    
    SRI --> SRI_WS
    SUNAT --> SUNAT_WS
    DIAN --> DIAN_WS
    SAT --> SAT_WS
```

## Adapter Pattern

### Common Interface
- `submitInvoice(invoice)`
- `checkAuthorization(submissionId)`
- `getAuthorizationDetails(authorizationId)`

### Country-Specific Implementation
- Country-specific web service integration
- Country-specific authentication
- Country-specific response handling

## Related Documents

- [Tax Authority Adapters](../integrations/tax-authority-adapters.md)
- [Multi-Country Strategy](../docs/multi-country-strategy.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team  
**Version:** 1.0
