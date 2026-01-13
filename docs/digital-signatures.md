# Digital Signatures

> **Icarus Nova** | Digital signature strategy for electronic invoices - XAdES, PKCS#7, and certificate management.

## Overview

This document describes the digital signature strategy for the Electronic Invoicing Platform. Digital signatures are critical for legal validity and regulatory compliance of electronic invoices.

## Digital Signature Standards

### XAdES (XML Advanced Electronic Signatures)

**Standard**: ETSI TS 101 903

**Characteristics:**
- XML-based signatures
- Advanced features (timestamping, revocation)
- Long-term validity
- Widely used in Latin America

**Usage:**
- Ecuador (SRI)
- Peru (SUNAT)
- Colombia (DIAN)
- Most Latin American countries

**Benefits:**
- Native XML support
- Advanced features
- Long-term validity
- Regulatory compliance

### PKCS#7 (Public Key Cryptography Standards)

**Standard**: RFC 2315, RFC 3852

**Characteristics:**
- Binary signature format
- Widely supported
- Certificate chain included
- Timestamping support

**Usage:**
- Some European countries
- Legacy systems
- Alternative to XAdES

**Benefits:**
- Wide compatibility
- Binary format
- Certificate chain
- Proven standard

## Signature Process

### 1. Certificate Management

**Certificate Requirements:**
- Valid certificate (not expired)
- Not revoked
- Appropriate key usage
- Trusted certificate authority

**Certificate Storage:**
- Secure storage (HSM, key vault)
- Encrypted at rest
- Access controls
- Audit logging

**Certificate Rotation:**
- Proactive rotation before expiration
- Graceful transition
- Old certificate retention (for validation)
- Automated rotation process

### 2. XML Preparation

**Process:**
- Generate canonical XML
- Apply canonicalization (C14N)
- Prepare for signing
- Ensure schema compliance

**Canonicalization:**
- Standardize XML format
- Remove formatting differences
- Preserve semantic meaning
- Ensure consistent signatures

### 3. Signature Application

**Process:**
- Load certificate and private key
- Calculate digest (hash)
- Sign digest with private key
- Embed signature in XML
- Add certificate chain
- Add timestamp (if required)

**Signature Algorithm:**
- RSA with SHA-256 (common)
- ECDSA with SHA-256 (modern)
- Algorithm selection based on certificate

### 4. Signature Validation

**Validation Steps:**
1. Extract signature from XML
2. Validate certificate
3. Verify certificate chain
4. Check certificate expiration
5. Check certificate revocation
6. Verify signature algorithm
7. Validate signature value
8. Verify timestamp (if present)

**Validation Result:**
- Valid: Signature is valid
- Invalid: Signature verification failed
- Expired: Certificate expired
- Revoked: Certificate revoked
- Unknown: Certificate not trusted

## Certificate Management

### Certificate Lifecycle

**Stages:**
1. **Provisioning**: Obtain certificate from CA
2. **Installation**: Install in secure storage
3. **Active**: Certificate in use
4. **Rotation**: Replace with new certificate
5. **Retired**: Certificate no longer used
6. **Archived**: Retained for validation

### Certificate Storage

**Storage Options:**

**Hardware Security Module (HSM):**
- Highest security
- Hardware-protected keys
- FIPS 140-2 Level 3+
- Cost: Higher

**Key Vault (Cloud):**
- Good security
- Managed service
- Scalable
- Cost: Moderate

**Software Key Store:**
- Basic security
- File-based storage
- Encrypted
- Cost: Lower

**Recommendation:**
- Production: HSM or Key Vault
- Development: Software Key Store
- High-security: HSM

### Certificate Rotation

**Rotation Strategy:**
- Proactive rotation (before expiration)
- Automated rotation process
- Graceful transition
- Old certificate retention

**Rotation Process:**
1. Obtain new certificate
2. Install new certificate
3. Update configuration
4. Test with new certificate
5. Switch to new certificate
6. Retain old certificate (for validation)
7. Archive old certificate

## Security Considerations

### Private Key Protection

**Requirements:**
- Never expose private key
- Encrypted storage
- Access controls
- Audit logging

**Protection Methods:**
- HSM protection
- Key vault encryption
- Access controls
- Audit trails

### Certificate Validation

**Validation Requirements:**
- Certificate not expired
- Certificate not revoked
- Valid certificate chain
- Trusted certificate authority

**Validation Process:**
- Check expiration date
- Check revocation status (OCSP/CRL)
- Validate certificate chain
- Verify trust anchor

### Timestamping

**Purpose:**
- Prove signature time
- Long-term validity
- Legal evidence

**Implementation:**
- Timestamp Authority (TSA)
- RFC 3161 compliant
- Timestamp embedded in signature
- Timestamp validation

## Signature Formats

### XAdES Enveloped

**Structure:**
- Signature embedded in XML
- Signature element in document
- Certificate chain included
- Timestamp included (if used)

**Example:**
```xml
<Invoice>
  <!-- Invoice content -->
  <ds:Signature>
    <ds:SignedInfo>
      <!-- Signature info -->
    </ds:SignedInfo>
    <ds:SignatureValue>...</ds:SignatureValue>
    <ds:KeyInfo>
      <ds:X509Data>
        <!-- Certificate -->
      </ds:X509Data>
    </ds:KeyInfo>
  </ds:Signature>
</Invoice>
```

### XAdES Detached

**Structure:**
- Signature separate from document
- Reference to document
- External signature file

**Usage:**
- When signature stored separately
- Batch signing
- External signature management

## Error Handling

### Signature Errors

**Common Errors:**
- Invalid certificate
- Expired certificate
- Revoked certificate
- Invalid signature algorithm
- Signature verification failure

**Handling:**
- Return clear error messages
- Log signature failures
- Alert on certificate issues
- Prevent invalid signatures

### Certificate Errors

**Common Errors:**
- Certificate not found
- Certificate expired
- Certificate revoked
- Invalid certificate format
- Certificate chain validation failure

**Handling:**
- Validate before use
- Proactive certificate management
- Automated certificate rotation
- Alert on certificate issues

## Compliance

### Regulatory Requirements

**Requirements:**
- Valid digital signature
- Certificate from trusted CA
- Long-term validity
- Legal evidence preservation

**Standards:**
- XAdES for Latin America
- eIDAS for Europe (where applicable)
- Country-specific requirements

### Audit Requirements

**Requirements:**
- Signature operation logging
- Certificate usage logging
- Signature validation logging
- Certificate rotation logging

## Performance Considerations

### Signature Performance

**Optimization:**
- Efficient signature algorithms
- Hardware acceleration (where available)
- Batch signing
- Async signing

**Targets:**
- Signature application: < 500ms
- Signature validation: < 200ms
- Certificate validation: < 100ms

## Related Documents

- [Security and Compliance](./security-and-compliance.md)
- [Invoice Lifecycle](./invoice-lifecycle.md)
- [ADR-0004: Digital Signature Strategy](../adr/0004-digital-signature-strategy.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team  
**Version:** 1.0
