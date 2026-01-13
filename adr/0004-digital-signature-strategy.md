# ADR-0004: Digital Signature Strategy

## Status

**Accepted** - This architectural decision ensures legal compliance.

## Context

Digital signatures are required for electronic invoices to be legally valid. We need to decide on signature standards, certificate management, and signature validation.

Options:
- XAdES (XML Advanced Electronic Signatures)
- PKCS#7
- Both (country-dependent)

## Decision

**We will use XAdES as the primary signature standard with PKCS#7 support where required.**

The platform will:

1. **XAdES Primary**: Use XAdES for XML signatures
2. **PKCS#7 Support**: Support PKCS#7 where required
3. **Certificate Management**: Secure certificate storage and rotation
4. **Signature Validation**: Comprehensive signature validation
5. **Long-Term Validity**: Ensure long-term signature validity

## Consequences

### Positive

✅ **Regulatory Compliance**: XAdES required in Latin America  
✅ **Legal Validity**: Ensures legal validity of invoices  
✅ **Long-Term Validity**: XAdES supports long-term validity  
✅ **Standard Compliance**: Industry-standard signature format  

### Negative

❌ **Complexity**: XAdES is complex  
❌ **Certificate Management**: Requires certificate management  
❌ **Performance**: Signature operations add latency  

### Mitigation

- Efficient signature libraries
- Hardware acceleration (where available)
- Good certificate management
- Performance optimization

## Implementation

### Signature Application

**Process:**
- Load certificate and private key
- Apply XAdES signature to XML
- Embed certificate chain
- Add timestamp (if required)
- Validate signature

### Certificate Management

**Requirements:**
- Secure certificate storage (HSM/Key Vault)
- Certificate rotation
- Certificate validation
- Certificate revocation checking

## Related Decisions

- [ADR-0002: XML as Source of Truth](./0002-xml-as-source-of-truth.md)
- [Digital Signatures](../docs/digital-signatures.md)

## References

- [Security and Compliance](../docs/security-and-compliance.md)

---

**Date**: 2026  
**Deciders**: Icarus Nova Architecture Team  
**Status**: Accepted
