# Invoice XML Example

> **Icarus Nova** | Example XML invoice document (conceptual, NOT production).

## Overview

This document shows an example XML invoice structure. This is a **conceptual example** for educational purposes.

## Example XML Structure

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Invoice xmlns="urn:oasis:names:specification:ubl:schema:xsd:Invoice-2">
  <cbc:ID>001-001-000000001</cbc:ID>
  <cbc:IssueDate>2024-01-15</cbc:IssueDate>
  <cbc:InvoiceTypeCode>01</cbc:InvoiceTypeCode>
  <cac:AccountingSupplierParty>
    <cac:Party>
      <cac:PartyIdentification>
        <cbc:ID>1234567890001</cbc:ID>
      </cac:PartyIdentification>
      <cac:PartyName>
        <cbc:Name>Example Company S.A.</cbc:Name>
      </cac:PartyName>
    </cac:Party>
  </cac:AccountingSupplierParty>
  <cac:AccountingCustomerParty>
    <cac:Party>
      <cac:PartyIdentification>
        <cbc:ID>9876543210001</cbc:ID>
      </cac:PartyIdentification>
      <cac:PartyName>
        <cbc:Name>Customer Company S.A.</cbc:Name>
      </cac:PartyName>
    </cac:Party>
  </cac:AccountingCustomerParty>
  <cac:InvoiceLine>
    <cbc:ID>1</cbc:ID>
    <cbc:InvoicedQuantity unitCode="C62">10</cbc:InvoicedQuantity>
    <cbc:LineExtensionAmount currencyID="USD">100.00</cbc:LineExtensionAmount>
    <cac:Item>
      <cbc:Description>Product Description</cbc:Description>
    </cac:Item>
    <cac:Price>
      <cbc:PriceAmount currencyID="USD">10.00</cbc:PriceAmount>
    </cac:Price>
  </cac:InvoiceLine>
  <cac:LegalMonetaryTotal>
    <cbc:LineExtensionAmount currencyID="USD">100.00</cbc:LineExtensionAmount>
    <cbc:TaxInclusiveAmount currencyID="USD">112.00</cbc:TaxInclusiveAmount>
    <cbc:PayableAmount currencyID="USD">112.00</cbc:PayableAmount>
  </cac:LegalMonetaryTotal>
</Invoice>
```

## Related Documents

- [Invoice Lifecycle](../docs/invoice-lifecycle.md)
- [ADR-0002: XML as Source of Truth](../adr/0002-xml-as-source-of-truth.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team
