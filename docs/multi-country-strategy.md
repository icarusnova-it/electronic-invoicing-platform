# Multi-Country Strategy

> **Icarus Nova** | Strategy for supporting multiple countries and tax authorities in a single platform.

## Overview

This document describes the strategy for supporting multiple countries and tax authorities in the Electronic Invoicing Platform. The strategy emphasizes a regulator-agnostic core with country-specific adapters, enabling rapid expansion to new countries while maintaining a consistent platform.

## Core Principles

### 1. Regulator-Agnostic Core

**Approach:**
- Core platform independent of specific tax authorities
- Common abstractions for regulatory concepts
- Shared business logic and workflows
- Country-agnostic data models

**Benefits:**
- Single codebase for core functionality
- Easier maintenance and updates
- Consistent behavior across countries
- Faster addition of new countries

### 2. Adapter Pattern

**Approach:**
- Country-specific logic in adapters
- Common adapter interface
- Pluggable adapters
- Easy adapter development

**Benefits:**
- Isolation of country-specific code
- Easy testing and maintenance
- Independent adapter updates
- Clear separation of concerns

### 3. Configuration-Driven

**Approach:**
- Country-specific configuration
- Feature flags by country
- Schema versioning
- Regulatory parameterization

**Benefits:**
- No code changes for configuration updates
- Easy A/B testing
- Gradual rollout
- Quick regulatory updates

## Architecture

### Core Platform

**Components:**
- Invoice domain model
- Business rules engine
- Validation framework
- Digital signature service
- Storage service
- Audit service
- API gateway

**Characteristics:**
- Country-agnostic
- Reusable across countries
- Extensible
- Well-tested

### Country Adapters

**Components:**
- Tax authority integration
- XML schema mapping
- Authorization handling
- Error message translation
- Country-specific validations

**Characteristics:**
- Country-specific
- Isolated from core
- Testable independently
- Versioned

### Configuration Layer

**Components:**
- Country configuration
- Schema versions
- Feature flags
- Regulatory parameters
- Business rules

**Characteristics:**
- Externalized configuration
- Runtime configurable
- Versioned
- Environment-specific

## Country Onboarding Process

### Phase 1: Analysis

**Activities:**
- Regulatory requirements analysis
- Tax authority integration analysis
- Schema analysis
- Common patterns identification
- Differences identification

**Deliverables:**
- Regulatory requirements document
- Integration specification
- Schema mapping
- Adapter design

### Phase 2: Adapter Development

**Activities:**
- Adapter implementation
- Schema mapping
- Integration development
- Validation rules
- Error handling

**Deliverables:**
- Country adapter
- Integration tests
- Documentation
- Configuration

### Phase 3: Testing

**Activities:**
- Unit testing
- Integration testing
- Tax authority sandbox testing
- End-to-end testing
- Performance testing

**Deliverables:**
- Test results
- Performance metrics
- Bug fixes
- Test documentation

### Phase 4: Deployment

**Activities:**
- Configuration deployment
- Adapter deployment
- Monitoring setup
- Documentation
- Training

**Deliverables:**
- Deployed adapter
- Monitoring dashboards
- User documentation
- Support documentation

## Common Abstractions

### Invoice Document

**Common Model:**
- Header (issuer, recipient, dates)
- Line items
- Taxes
- Totals
- Payment information

**Country Mapping:**
- Map common model to country-specific XML
- Handle country-specific fields
- Preserve data integrity

### Tax Authority

**Common Interface:**
- Submit invoice
- Check authorization status
- Get authorization details
- Handle errors

**Country Implementation:**
- Country-specific web service integration
- Country-specific authentication
- Country-specific response handling

### Authorization

**Common Model:**
- Authorization number
- Authorization date
- Authorization status
- Error messages

**Country Mapping:**
- Map country-specific response to common model
- Handle country-specific statuses
- Translate error messages

## Configuration Management

### Country Configuration

**Configuration Structure:**
```json
{
  "country": "EC",
  "taxAuthority": "SRI",
  "schemaVersion": "2.1",
  "xmlFormat": "UBL",
  "signatureStandard": "XAdES",
  "authorizationType": "async",
  "retentionYears": 7,
  "features": {
    "withholdingTax": true,
    "creditNotes": true,
    "debitNotes": true
  }
}
```

### Feature Flags

**Usage:**
- Enable/disable features by country
- Gradual feature rollout
- A/B testing
- Emergency feature disable

**Examples:**
- New authorization flow
- Enhanced validation
- New document types
- Performance optimizations

### Schema Versioning

**Strategy:**
- Support multiple schema versions
- Version-specific adapters
- Gradual migration
- Backward compatibility

**Management:**
- Schema version per country
- Version mapping
- Migration scripts
- Deprecation notices

## Adapter Development

### Adapter Interface

**Required Methods:**
- `submitInvoice(invoice)`: Submit invoice to tax authority
- `checkAuthorization(submissionId)`: Check authorization status
- `getAuthorizationDetails(authorizationId)`: Get authorization details
- `validateInvoice(invoice)`: Country-specific validation

### Adapter Implementation

**Structure:**
- Tax authority client
- XML transformation
- Response mapping
- Error handling
- Retry logic

### Adapter Testing

**Test Types:**
- Unit tests
- Integration tests (sandbox)
- End-to-end tests
- Performance tests

**Test Data:**
- Valid invoices
- Invalid invoices
- Edge cases
- Error scenarios

## Regulatory Updates

### Update Detection

**Methods:**
- Manual monitoring
- Automated monitoring
- Customer notifications
- Regulatory announcements

### Update Process

**Steps:**
1. Regulatory change identified
2. Impact analysis
3. Adapter update or configuration change
4. Testing
5. Deployment
6. Monitoring

### Version Management

**Strategy:**
- Support multiple versions during transition
- Gradual migration
- Backward compatibility
- Clear versioning

## Multi-Tenant Considerations

### Tenant Isolation

**Requirements:**
- Data isolation per tenant
- Configuration per tenant
- Country selection per tenant
- Access controls per tenant

### Tenant Configuration

**Configuration:**
- Enabled countries
- Tax authority credentials
- Certificate management
- Feature access

## Performance and Scalability

### Scaling Strategy

**Horizontal Scaling:**
- Stateless adapters
- Load balancing
- Auto-scaling
- Distributed processing

### Performance Optimization

**Strategies:**
- Caching
- Batch processing
- Async processing
- Connection pooling

## Monitoring and Observability

### Metrics

**Country-Specific Metrics:**
- Invoice volume per country
- Authorization success rate per country
- Response times per country
- Error rates per country

### Logging

**Logging:**
- Country identification
- Adapter version
- Configuration version
- Operation traces

## Related Documents

- [Regulatory Overview](./regulatory-overview.md)
- [Invoice Lifecycle](./invoice-lifecycle.md)
- [ADR-0001: Regulator-Agnostic Design](../adr/0001-regulator-agnostic-design.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team  
**Version:** 1.0
