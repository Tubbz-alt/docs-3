# Credit

## Creating Credit Classes

```
scalar CreditClassID

tx CreateCreditClass(
  classMetadata data.HashIRI,
  issuers Address*,
  creditMetadataClass data.HashIRI,
  validationScript script.ScriptID?
) CreditClassID
```

## Issuing Credits


```
tx IssueCredit(
  cls CreditClassID,
  holder Address,
  liquidUnits Decimal,
  burnedUnits Decimal,
  metadata data.HashIRI
) AssetID
```

## Sending and Burning (Retiring) Credits

Sending and burning (or retiring) of credits is done via the bank.Send and
bank.Burn transactions.

## State

```text
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



