# Credit

```text
module Credit

scalar CreditClassID

tx CreateCreditClass(
  classMetadata data.HashIRI,
  issuers Address*,
  creditMetadataClass data.HashIRI,
  validationScript script.ScriptID?
) CreditClassID
  
tx IssueCredit(
  cls CreditClassID,
  holder Address,
  liquidUnits Decimal,
  burnedUnits Decimal,
  metadata data.HashIRI
) AssetID

table CreditClass {
  id: uint64
  metadata: data.HashIRI
  designer: Address
  issuers: Address*
  validationScript: script.ScriptID?
  @auto_primary_key(id)
  @index(designer)
  @multi_index(issuers)
}
```



