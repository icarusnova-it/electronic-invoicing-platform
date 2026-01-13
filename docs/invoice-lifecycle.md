# Invoice Lifecycle

> **Icarus Nova** | Complete lifecycle of an electronic invoice from creation to archival.

## Overview

This document describes the complete lifecycle of an electronic invoice in the platform, from creation through validation, signing, authorization, storage, and archival. Understanding this lifecycle is critical for designing a robust, compliant platform.

## Lifecycle Stages

### 1. Invoice Creation

**Input:**
- Invoice data from ERP/business system
- Customer information
- Line items
- Tax information
- Payment terms

**Process:**
- Receive invoice data via API
- Validate business rules
- Generate invoice number (if not provided)
- Create invoice document structure
- Assign unique invoice identifier

**Output:**
- Invoice document (internal format)
- Invoice identifier
- Creation timestamp

**Validation:**
- Required fields present
- Data format validation
- Business rule validation
- Tax calculation validation

### 2. Invoice Validation

**Validation Levels:**

**Business Validation:**
- Required fields present
- Data types correct
- Value ranges valid
- Business rules satisfied

**Regulatory Validation:**
- Country-specific rules
- Tax authority requirements
- Schema validation
- Regulatory compliance

**Technical Validation:**
- XML structure valid
- Schema compliance
- Character encoding
- Data integrity

**Process:**
- Apply validation rules
- Check country-specific requirements
- Validate tax calculations
- Verify document structure

**Output:**
- Validation result (success/failure)
- Validation errors (if any)
- Validation timestamp

### 3. XML Generation

**Process:**
- Transform internal invoice to XML
- Apply country-specific XML schema
- Generate UBL or country-specific format
- Validate XML structure
- Ensure schema compliance

**Output:**
- XML document
- XML validation result
- Generation timestamp

**Standards:**
- UBL 2.1 (Universal Business Language)
- Country-specific schemas
- XML Schema Definition (XSD)

### 4. Digital Signature

**Process:**
- Load digital certificate
- Apply digital signature to XML
- Use XAdES or PKCS#7 standard
- Add timestamp (if required)
- Validate signature

**Signature Requirements:**
- Certificate-based signature
- Valid certificate (not expired, not revoked)
- Signature algorithm (RSA, ECDSA)
- Signature format (XAdES, PKCS#7)

**Output:**
- Signed XML document
- Signature metadata
- Signature timestamp
- Certificate information

**Security:**
- Certificate stored securely
- Private key protection
- Signature validation
- Certificate rotation

### 5. Submission to Tax Authority

**Process:**
- Select appropriate tax authority adapter
- Transform to tax authority format (if needed)
- Authenticate with tax authority
- Submit invoice via web service
- Receive submission acknowledgment

**Submission Methods:**
- **SOAP Web Service**: Traditional method
- **REST API**: Modern method (increasing)
- **File Upload**: Batch processing
- **Real-Time**: Immediate submission

**Authentication:**
- Certificate-based authentication
- API keys/tokens
- OAuth (where supported)

**Output:**
- Submission acknowledgment
- Submission ID
- Submission timestamp
- Tax authority response (if synchronous)

### 6. Authorization

**Authorization Types:**

**Synchronous Authorization:**
- Immediate response from tax authority
- Authorization number provided
- Status (authorized/rejected)
- Error messages (if rejected)

**Asynchronous Authorization:**
- Submission acknowledgment
- Authorization via callback/webhook
- Polling for status (fallback)
- Authorization number when ready

**Process:**
- Wait for tax authority response
- Handle timeout scenarios
- Process authorization response
- Update invoice status
- Store authorization details

**Output:**
- Authorization status
- Authorization number
- Authorization date
- Error messages (if rejected)

### 7. Retry and Error Handling

**Retry Scenarios:**
- Network failures
- Tax authority timeouts
- Temporary service unavailability
- Rate limiting

**Retry Strategy:**
- Exponential backoff
- Maximum retry attempts
- Retry queue management
- Dead letter queue for failures

**Error Handling:**
- Validation errors: Return to user
- Signature errors: Retry with valid certificate
- Submission errors: Retry submission
- Authorization errors: Handle rejection

### 8. Storage

**Storage Requirements:**
- Original signed XML
- PDF representation (if generated)
- Authorization response
- Audit trail
- Metadata

**Storage Strategy:**
- Immutable storage
- Version control
- Legal retention period
- Secure storage
- Backup and replication

**Retention:**
- 5-7 years (country-dependent)
- Original format preservation
- Access controls
- Audit logging

### 9. Distribution

**Distribution Methods:**
- Email to customer
- Download via portal
- API delivery
- Integration with business systems

**Distribution Formats:**
- Signed XML (original)
- PDF (human-readable)
- JSON (for integration)

**Process:**
- Generate PDF (if needed)
- Send to customer
- Log distribution
- Track delivery

### 10. Audit and Traceability

**Audit Requirements:**
- All operations logged
- Immutable audit trail
- Operation timestamps
- User/system identification
- Operation details

**Traceability:**
- Invoice creation to archival
- All state changes
- All user actions
- All system operations
- Complete operation history

## State Machine

### Invoice States

```
CREATED → VALIDATED → SIGNED → SUBMITTED → AUTHORIZED → STORED → ARCHIVED
   ↓         ↓          ↓          ↓            ↓          ↓
 REJECTED  REJECTED   REJECTED   REJECTED     REJECTED
```

**State Transitions:**
- **CREATED**: Invoice created, awaiting validation
- **VALIDATED**: Validation passed, ready for signing
- **SIGNED**: Digital signature applied
- **SUBMITTED**: Submitted to tax authority
- **AUTHORIZED**: Authorized by tax authority
- **REJECTED**: Rejected at any stage
- **STORED**: Stored for retention
- **ARCHIVED**: Archived after retention period

## Error Scenarios

### Validation Errors

**Handling:**
- Return errors to user
- Allow correction
- Re-validate after correction
- Prevent progression until valid

### Signature Errors

**Handling:**
- Certificate issues: Use valid certificate
- Signature algorithm: Use supported algorithm
- Timestamp issues: Retry with valid timestamp
- Validation failures: Fix and re-sign

### Submission Errors

**Handling:**
- Network errors: Retry with backoff
- Authentication errors: Verify credentials
- Format errors: Validate and fix
- Rate limiting: Implement backoff

### Authorization Errors

**Handling:**
- Rejection: Handle rejection reason
- Timeout: Retry or poll for status
- Service unavailable: Retry later
- Permanent failure: Dead letter queue

## Performance Considerations

### Processing Time

- **Creation**: < 100ms
- **Validation**: < 200ms
- **XML Generation**: < 300ms
- **Signing**: < 500ms
- **Submission**: < 2s (network dependent)
- **Authorization**: Variable (tax authority dependent)

### Throughput

- **Target**: 10,000+ invoices/hour
- **Peak**: 50,000+ invoices/hour
- **Scaling**: Horizontal scaling
- **Optimization**: Batch processing, async operations

## Related Documents

- [Regulatory Overview](./regulatory-overview.md)
- [Multi-Country Strategy](./multi-country-strategy.md)
- [Digital Signatures](./digital-signatures.md)
- [Invoice Flow Diagram](../diagrams/invoice-flow.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team  
**Version:** 1.0
