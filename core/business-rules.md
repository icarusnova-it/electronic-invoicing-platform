# Business Rules

> **Icarus Nova** | Business rules and validation logic for electronic invoices.

## Overview

This document describes the business rules and validation logic for the Electronic Invoicing Platform. Rules are organized by category and can be configured per country.

## Validation Rules

### Invoice Validation

**Required Fields:**
- Invoice number
- Invoice date
- Issuer information
- Recipient information
- At least one line item
- Totals

**Business Rules:**
- Invoice number must be unique per organization
- Invoice date cannot be in the future
- Totals must match line items
- Tax calculations must be correct

### Tax Validation

**Tax Rules:**
- Tax rates must be valid for country
- Tax calculations must be accurate
- Withholding tax rules (country-specific)
- Special tax regimes (country-specific)

### Regulatory Validation

**Country-Specific Rules:**
- Schema validation
- Regulatory requirements
- Tax authority rules
- Document format requirements

## Related Documents

- [Domain Model](./domain-model.md)
- [Regulatory Overview](../docs/regulatory-overview.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team  
**Version:** 1.0
