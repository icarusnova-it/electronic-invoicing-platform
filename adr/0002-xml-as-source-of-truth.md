# ADR-0002: XML as Source of Truth

## Status

**Accepted** - This is a fundamental architectural decision for legal compliance.

## Context

Electronic invoices can be represented in multiple formats (XML, PDF, JSON). We need to decide which format is the authoritative source of truth for legal and compliance purposes.

Options:
- XML as source of truth
- JSON as source of truth
- Multiple sources of truth
- Database as source of truth

## Decision

**XML (signed) is the source of truth for electronic invoices.**

The platform will:

1. **XML Generation**: Generate XML from internal model
2. **Digital Signature**: Sign XML with digital signature
3. **XML Storage**: Store signed XML as authoritative document
4. **PDF Generation**: Generate PDF from XML for human readability
5. **Database Metadata**: Store metadata in database, but XML is authoritative

## Consequences

### Positive

✅ **Legal Compliance**: XML is required by tax authorities  
✅ **Digital Signature**: XML supports digital signatures (XAdES)  
✅ **Immutable Evidence**: Signed XML is legal evidence  
✅ **Regulatory Compliance**: Meets tax authority requirements  
✅ **Long-Term Validity**: XML format ensures long-term accessibility  

### Negative

❌ **XML Complexity**: XML is more complex than JSON  
❌ **Processing Overhead**: XML parsing overhead  
❌ **Storage Size**: XML files larger than JSON  

### Mitigation

- Efficient XML processing
- Compression for storage
- Clear XML schema
- Good tooling support

## Implementation

### XML Generation

**Process:**
- Transform internal invoice model to XML
- Apply country-specific XML schema
- Validate XML structure
- Ensure schema compliance

### Digital Signature

**Process:**
- Apply digital signature to XML
- Use XAdES standard
- Embed certificate chain
- Add timestamp (if required)

### Storage

**Storage Strategy:**
- Store signed XML as primary document
- Generate PDF from XML (for readability)
- Store metadata in database
- XML is authoritative for legal purposes

## Related Decisions

- [ADR-0001: Regulator-Agnostic Design](./0001-regulator-agnostic-design.md)
- [ADR-0004: Digital Signature Strategy](./0004-digital-signature-strategy.md)
- [Digital Signatures](../docs/digital-signatures.md)

## References

- [Invoice Lifecycle](../docs/invoice-lifecycle.md)
- [Storage Strategy](../storage/document-storage-strategy.md)

---

**Date**: 2024  
**Deciders**: Icarus Nova Architecture Team  
**Status**: Accepted
