# Regulatory Overview

> **Icarus Nova** | Understanding tax authority regulations and common patterns across countries.

## Overview

This document provides an overview of electronic invoicing regulations across different countries, identifying common patterns and differences. This understanding is critical for designing a regulator-agnostic platform that can adapt to multiple jurisdictions.

## Common Regulatory Patterns

### 1. Invoice Structure

**Common Elements:**
- **Issuer Information**: Tax ID, name, address
- **Recipient Information**: Tax ID, name, address
- **Invoice Details**: Number, date, currency
- **Line Items**: Products/services, quantities, prices
- **Taxes**: VAT, sales tax, withholdings
- **Totals**: Subtotal, taxes, total
- **Payment Information**: Payment methods, terms

**Format Standards:**
- XML-based formats (UBL, FacturaE, etc.)
- Structured data for machine processing
- Human-readable formats (PDF) for presentation

### 2. Digital Signatures

**Common Requirements:**
- Digital signature on invoice XML
- Certificate-based signatures (XAdES, PKCS#7)
- Certificate validation
- Signature timestamping
- Long-term signature validity

**Standards:**
- XAdES (XML Advanced Electronic Signatures)
- PKCS#7 (Public Key Cryptography Standards)
- Certificate authority validation

### 3. Authorization Process

**Common Flow:**
1. Invoice creation and validation
2. Digital signature application
3. Submission to tax authority
4. Authorization response
5. Storage and distribution

**Authorization Types:**
- **Synchronous**: Immediate response (less common)
- **Asynchronous**: Response via callback/webhook (common)
- **Batch**: Multiple invoices in one request

### 4. Tax Authority Integration

**Common Integration Methods:**
- **SOAP Web Services**: Traditional integration
- **REST APIs**: Modern integration (increasing)
- **File Upload**: Batch processing
- **Real-Time**: Immediate processing

**Authentication:**
- Certificate-based authentication
- API keys/tokens
- OAuth (increasing adoption)

## Country-Specific Regulations

### Ecuador (SRI - Servicio de Rentas Internas)

**Regulation**: Resolución NAC-DGERCGC16-00000420

**Key Requirements:**
- XML format (UBL 2.1)
- Digital signature (XAdES)
- Authorization via SRI web services
- Authorization number (número de autorización)
- Retention period: 7 years

**Integration:**
- SOAP web services
- Certificate-based authentication
- Asynchronous authorization

**Special Considerations:**
- Withholding tax (retención)
- Special tax regimes
- Offline mode support

### Peru (SUNAT - Superintendencia Nacional de Aduanas y de Administración Tributaria)

**Regulation**: Resolución de Superintendencia N° 097-2012

**Key Requirements:**
- XML format (UBL 2.1)
- Digital signature (XAdES)
- Authorization via SUNAT web services
- Authorization number (número de autorización)
- Retention period: 5 years

**Integration:**
- SOAP web services
- Certificate-based authentication
- Asynchronous authorization

**Special Considerations:**
- Electronic receipts (boletas)
- Electronic invoices (facturas)
- Different document types

### Colombia (DIAN - Dirección de Impuestos y Aduanas Nacionales)

**Regulation**: Resolución 000042 de 2020

**Key Requirements:**
- XML format (UBL 2.1)
- Digital signature (XAdES)
- Authorization via DIAN web services
- Authorization number (CUFE - Código Único de Facturación Electrónica)
- Retention period: 5 years

**Integration:**
- SOAP web services
- Certificate-based authentication
- Asynchronous authorization

**Special Considerations:**
- CUFE generation
- Event status (eventos)
- Credit notes and debit notes

### Mexico (SAT - Servicio de Administración Tributaria)

**Regulation**: Resolución Miscelánea Fiscal

**Key Requirements:**
- XML format (CFDI - Comprobante Fiscal Digital por Internet)
- Digital signature (XAdES)
- Authorization via PAC (Proveedor Autorizado de Certificación)
- Authorization number (UUID)
- Retention period: 5 years

**Integration:**
- SOAP web services (PAC)
- Certificate-based authentication
- PAC intermediaries

**Special Considerations:**
- PAC intermediaries required
- UUID generation
- Multiple PAC providers

### Chile (SII - Servicio de Impuestos Internos)

**Regulation**: Resolución Exenta N° 66

**Key Requirements:**
- XML format
- Digital signature
- Authorization via SII web services
- Authorization number (folio)
- Retention period: 6 years

**Integration:**
- SOAP web services
- Certificate-based authentication
- Asynchronous authorization

**Special Considerations:**
- Folio allocation
- Electronic receipts (boletas)
- Electronic invoices (facturas)

## Common Abstractions

### Invoice Document

**Common Structure:**
- Header (issuer, recipient, dates)
- Line items (products/services)
- Taxes (VAT, sales tax, withholdings)
- Totals
- Payment information
- Additional information

### Authorization

**Common Elements:**
- Authorization number
- Authorization date
- Authorization status
- Error messages (if rejected)
- Additional metadata

### Digital Signature

**Common Requirements:**
- Certificate-based signature
- Signature algorithm
- Timestamp
- Signature validation

## Regulatory Differences

### Format Variations

- **XML Schemas**: Different XSD schemas per country
- **UBL Versions**: Different UBL versions
- **Custom Formats**: Country-specific formats

### Authorization Flow

- **Synchronous vs. Asynchronous**: Different response patterns
- **Batch Processing**: Some countries support batch, others don't
- **Retry Logic**: Different retry requirements

### Tax Calculations

- **VAT Rates**: Different rates and rules
- **Withholding Tax**: Different withholding requirements
- **Special Regimes**: Country-specific tax regimes

### Retention Requirements

- **Retention Period**: 5-7 years typically
- **Storage Format**: Original XML + PDF
- **Access Requirements**: Audit access requirements

## Platform Abstraction Strategy

### Core Abstractions

**Invoice Document:**
- Common invoice model
- Country-specific mapping
- Validation rules

**Tax Authority:**
- Abstract tax authority interface
- Country-specific adapters
- Common integration patterns

**Authorization:**
- Common authorization model
- Country-specific response handling
- Status mapping

### Adapter Pattern

**Implementation:**
- Core platform independent of country
- Country-specific adapters
- Common interfaces
- Easy addition of new countries

## Regulatory Updates

### Update Frequency

- **Regular Updates**: Quarterly or semi-annually
- **Emergency Updates**: As needed for compliance
- **Version Management**: Schema versioning

### Update Strategy

- **Versioning**: Support multiple schema versions
- **Feature Flags**: Enable/disable features by country
- **Backward Compatibility**: Maintain compatibility where possible

## Compliance Requirements

### Legal Requirements

- **Document Integrity**: Immutable documents
- **Audit Trails**: Complete operation logs
- **Legal Evidence**: Preserve legal evidence
- **Access Controls**: Secure access to documents

### Technical Requirements

- **Digital Signatures**: Valid signatures
- **Certificate Management**: Secure certificate storage
- **Encryption**: Encrypted storage and transmission
- **Availability**: High availability for critical operations

## Related Documents

- [Multi-Country Strategy](./multi-country-strategy.md)
- [Invoice Lifecycle](./invoice-lifecycle.md)
- [Digital Signatures](./digital-signatures.md)
- [ADR-0001: Regulator-Agnostic Design](../adr/0001-regulator-agnostic-design.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team  
**Version:** 1.0
