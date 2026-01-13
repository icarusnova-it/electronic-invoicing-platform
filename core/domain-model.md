# Domain Model

> **Icarus Nova** | Core domain entities and their relationships.

## Overview

This document describes the core domain model for the Electronic Invoicing Platform. The domain model is regulator-agnostic and represents common concepts across countries.

## Core Entities

### Invoice

**Purpose:** Represents an electronic invoice

**Attributes:**
- Invoice ID
- Invoice number
- Organization
- Country
- Issuer information
- Recipient information
- Invoice date
- Line items
- Taxes
- Totals
- Status

### LineItem

**Purpose:** Represents a line item in an invoice

**Attributes:**
- Line item ID
- Product/service code
- Description
- Quantity
- Unit price
- Discount
- Subtotal
- Taxes
- Total

### Tax

**Purpose:** Represents tax information

**Attributes:**
- Tax type (VAT, sales tax, withholding)
- Tax rate
- Taxable amount
- Tax amount
- Tax code

### Authorization

**Purpose:** Represents tax authority authorization

**Attributes:**
- Authorization number
- Authorization date
- Status
- Tax authority
- Error messages (if rejected)

## Relationships

- Invoice has many LineItems
- Invoice has one Authorization
- LineItem has many Taxes
- Invoice belongs to Organization

## Related Documents

- [Data Model Overview](../docs/data-model-overview.md)
- [Business Rules](./business-rules.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team  
**Version:** 1.0
