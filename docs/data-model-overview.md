# Data Model Overview

> **Icarus Nova** | Core data models and domain entities for the electronic invoicing platform.

## Overview

This document provides an overview of the core data models in the Electronic Invoicing Platform. These models represent the domain entities and their relationships, forming the foundation of the platform's data architecture.

## Core Entities

### Invoice

**Purpose:** Represents an electronic invoice document

**Attributes:**
- `invoiceId`: Unique identifier
- `invoiceNumber`: Invoice number (business identifier)
- `organizationId`: Organization that issued the invoice
- `country`: Country code
- `taxAuthority`: Tax authority code
- `issuer`: Issuer information (tax ID, name, address)
- `recipient`: Recipient information (tax ID, name, address)
- `invoiceDate`: Invoice date
- `dueDate`: Due date
- `currency`: Currency code
- `lineItems`: Array of line items
- `taxes`: Tax information
- `totals`: Invoice totals
- `paymentInfo`: Payment information
- `status`: Invoice status
- `createdAt`: Creation timestamp
- `updatedAt`: Last update timestamp

**Relationships:**
- Belongs to Organization
- Has many LineItems
- Has one Authorization
- Has many AuditEvents

### LineItem

**Purpose:** Represents a line item in an invoice

**Attributes:**
- `lineItemId`: Unique identifier
- `invoiceId`: Parent invoice ID
- `lineNumber`: Line number
- `productCode`: Product/service code
- `description`: Product/service description
- `quantity`: Quantity
- `unitPrice`: Unit price
- `discount`: Discount amount
- `subtotal`: Line subtotal
- `taxes`: Tax information for line
- `total`: Line total

**Relationships:**
- Belongs to Invoice
- Has many Taxes

### Tax

**Purpose:** Represents tax information

**Attributes:**
- `taxId`: Unique identifier
- `invoiceId`: Parent invoice ID (if invoice-level tax)
- `lineItemId`: Parent line item ID (if line-level tax)
- `taxType`: Tax type (VAT, sales tax, withholding, etc.)
- `taxRate`: Tax rate
- `taxableAmount`: Taxable amount
- `taxAmount`: Tax amount
- `taxCode`: Tax code

**Relationships:**
- Belongs to Invoice or LineItem

### Authorization

**Purpose:** Represents tax authority authorization

**Attributes:**
- `authorizationId`: Unique identifier
- `invoiceId`: Related invoice ID
- `authorizationNumber`: Authorization number from tax authority
- `authorizationDate`: Authorization date
- `status`: Authorization status (pending, authorized, rejected)
- `taxAuthority`: Tax authority code
- `submissionId`: Submission ID to tax authority
- `response`: Full response from tax authority
- `errorMessage`: Error message (if rejected)
- `createdAt`: Creation timestamp
- `updatedAt`: Last update timestamp

**Relationships:**
- Belongs to Invoice

### Organization

**Purpose:** Represents an organization using the platform

**Attributes:**
- `organizationId`: Unique identifier
- `name`: Organization name
- `taxId`: Tax identification number
- `country`: Country code
- `enabledCountries`: Array of enabled countries
- `certificates`: Digital certificates
- `configuration`: Organization-specific configuration
- `createdAt`: Creation timestamp
- `updatedAt`: Last update timestamp

**Relationships:**
- Has many Invoices
- Has many Certificates
- Has many Users

### Certificate

**Purpose:** Represents a digital certificate for signing

**Attributes:**
- `certificateId`: Unique identifier
- `organizationId`: Organization that owns the certificate
- `country`: Country code
- `certificateData`: Certificate data (encrypted)
- `privateKey`: Private key (encrypted, secure storage)
- `serialNumber`: Certificate serial number
- `issuer`: Certificate issuer
- `validFrom`: Certificate valid from date
- `validTo`: Certificate valid to date
- `status`: Certificate status (active, expired, revoked)
- `createdAt`: Creation timestamp
- `updatedAt`: Last update timestamp

**Relationships:**
- Belongs to Organization

### AuditEvent

**Purpose:** Represents an audit event

**Attributes:**
- `auditEventId`: Unique identifier
- `invoiceId`: Related invoice ID (if applicable)
- `organizationId`: Organization ID
- `eventType`: Event type
- `eventData`: Event data (JSON)
- `userId`: User ID (if user action)
- `systemId`: System ID (if system action)
- `timestamp`: Event timestamp
- `ipAddress`: IP address
- `userAgent`: User agent

**Relationships:**
- Belongs to Invoice (optional)
- Belongs to Organization

### Document

**Purpose:** Represents stored documents (XML, PDF)

**Attributes:**
- `documentId`: Unique identifier
- `invoiceId`: Related invoice ID
- `documentType`: Document type (xml, pdf, etc.)
- `storageLocation`: Storage location (S3, blob storage, etc.)
- `storageKey`: Storage key
- `contentHash`: Content hash (SHA-256)
- `size`: Document size in bytes
- `mimeType`: MIME type
- `createdAt`: Creation timestamp

**Relationships:**
- Belongs to Invoice

## Data Relationships

### Entity Relationship Diagram

```
Organization
    ├── has many Invoices
    ├── has many Certificates
    └── has many Users

Invoice
    ├── belongs to Organization
    ├── has many LineItems
    ├── has one Authorization
    ├── has many Documents
    └── has many AuditEvents

LineItem
    ├── belongs to Invoice
    └── has many Taxes

Tax
    ├── belongs to Invoice (optional)
    └── belongs to LineItem (optional)

Authorization
    └── belongs to Invoice

Document
    └── belongs to Invoice

AuditEvent
    ├── belongs to Invoice (optional)
    └── belongs to Organization

Certificate
    └── belongs to Organization
```

## Data Storage Strategy

### Primary Database

**Storage:**
- Invoice metadata
- Authorization information
- Organization data
- Certificate metadata
- Audit events

**Technology:**
- PostgreSQL (relational database)
- ACID transactions
- Encryption at rest
- Backup and replication

### Document Storage

**Storage:**
- XML documents (signed)
- PDF documents
- Other document formats

**Technology:**
- Object storage (S3, Blob Storage)
- Immutable storage
- Version control
- Legal retention

### Cache

**Storage:**
- Frequently accessed data
- Authorization status
- Configuration data
- Temporary data

**Technology:**
- Redis
- High performance
- TTL management
- Clustering support

## Data Retention

### Retention Policy

**Invoice Data:**
- Metadata: 7 years (legal requirement)
- Documents: 7 years (legal requirement)
- Audit events: 7 years (legal requirement)

**Organization Data:**
- Active organizations: Indefinite
- Inactive organizations: 90 days after deactivation

**Certificate Data:**
- Active certificates: Duration of validity
- Expired certificates: 7 years (for validation)

## Data Security

### Encryption

**At Rest:**
- Database encryption (AES-256)
- Document encryption
- Certificate encryption
- Key management

**In Transit:**
- TLS 1.3+ for all communications
- Encrypted API calls
- Secure document transfer

### Access Controls

**Data Access:**
- Role-based access control
- Organization-level isolation
- Resource-level permissions
- Audit logging

## Data Migration

### Migration Strategy

**Approaches:**
- Zero-downtime migration
- Data validation
- Rollback capability
- Migration monitoring

**Process:**
- Schema migration
- Data migration
- Validation
- Rollback plan

## Related Documents

- [Core Domain Model](../core/domain-model.md)
- [Business Rules](../core/business-rules.md)
- [Storage Strategy](../storage/document-storage-strategy.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team  
**Version:** 1.0
