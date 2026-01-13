# Core Platform

> **Icarus Nova** | Core domain model and business rules for the electronic invoicing platform.

## Overview

The core platform contains the domain model and business rules that are independent of specific tax authorities. This is the foundation of the regulator-agnostic design.

## Components

### Domain Model

See [Domain Model](./domain-model.md) for detailed domain entities and relationships.

### Business Rules

See [Business Rules](./business-rules.md) for business logic and validation rules.

## Key Principles

### 1. Regulator-Agnostic

- Core platform independent of tax authorities
- Common abstractions for regulatory concepts
- Country-specific logic in adapters

### 2. Domain-Driven Design

- Rich domain model
- Business logic in domain
- Clear boundaries
- Ubiquitous language

### 3. Business Rules Engine

- Configurable business rules
- Country-specific rules via configuration
- Validation framework
- Extensible rules

## Related Documents

- [Domain Model](./domain-model.md)
- [Business Rules](./business-rules.md)
- [Data Model Overview](../docs/data-model-overview.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team  
**Version:** 1.0
