# ADR-0001: Regulator-Agnostic Design

## Status

**Accepted** - This is a fundamental architectural decision that cannot be changed without significant impact.

## Context

Electronic invoicing platforms face a critical decision: whether to design for a specific tax authority (e.g., SRI Ecuador) or design a platform that can support multiple tax authorities across different countries.

Country-specific solutions:
- Faster initial development
- Tight coupling to specific regulator
- Difficult to expand to new countries
- High maintenance cost per country

We need to decide on our architectural approach for multi-country support.

## Decision

**We will design a regulator-agnostic core platform with country-specific adapters.**

The platform will:

1. **Core Platform**: Independent of specific tax authorities
2. **Adapter Pattern**: Country-specific logic in adapters
3. **Common Abstractions**: Shared concepts across countries
4. **Configuration-Driven**: Country-specific behavior via configuration
5. **Easy Expansion**: New countries added via adapters

## Consequences

### Positive

✅ **Multi-Country Support**: Single platform for multiple countries  
✅ **Maintainability**: Core logic shared, country-specific isolated  
✅ **Scalability**: Platform scales across countries  
✅ **Time to Market**: Faster addition of new countries  
✅ **Cost Efficiency**: Reduced development and maintenance costs  
✅ **Competitive Advantage**: Multi-country capability  

### Negative

❌ **Initial Complexity**: More complex initial design  
❌ **Abstraction Overhead**: Additional abstraction layer  
❌ **Testing Complexity**: Testing across multiple countries  

### Mitigation

- Clear abstraction boundaries
- Comprehensive testing strategy
- Well-documented adapter interface
- Configuration management

## Implementation

### Core Platform

**Components:**
- Invoice domain model
- Business rules engine
- Validation framework
- Digital signature service
- Storage service
- Audit service

**Characteristics:**
- Country-agnostic
- Reusable
- Extensible
- Well-tested

### Adapter Pattern

**Adapter Interface:**
- `submitInvoice(invoice)`
- `checkAuthorization(submissionId)`
- `getAuthorizationDetails(authorizationId)`
- `validateInvoice(invoice)`

**Country Adapters:**
- SRI Adapter (Ecuador)
- SUNAT Adapter (Peru)
- DIAN Adapter (Colombia)
- SAT Adapter (Mexico)
- Additional countries as needed

### Configuration

**Country Configuration:**
- Schema versions
- Feature flags
- Regulatory parameters
- Business rules

## Related Decisions

- [ADR-0002: XML as Source of Truth](./0002-xml-as-source-of-truth.md)
- [ADR-0003: Asynchronous Authorization](./0003-asynchronous-authorization.md)
- [Multi-Country Strategy](../docs/multi-country-strategy.md)

## References

- [Regulatory Overview](../docs/regulatory-overview.md)
- [Product Vision](../docs/product-vision.md)

---

**Date**: 2024  
**Deciders**: Icarus Nova Architecture Team  
**Status**: Accepted
