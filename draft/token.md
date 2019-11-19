# Credit

## Creating Credit Classes

```text
scalar CreditClassID

tx CreateCreditClass(
  classMetadata data.HashURI,
  issuers Address*,
  creditMetadataClass data.HashURI,
  validationScript script.ScriptID?
) CreditClassID
```

## Issuing Credits

```text
tx IssueCredit(
  cls CreditClassID,
  holder Address,
  liquidUnits Decimal,
  burnedUnits Decimal,
  metadata data.HashURI
) AssetID
```

```text
IssueCredit(
  CarbonCredit,
  SomeUser,
  100,
  0,
  HashURI("Qmsdgknwetinsdgsdgi"))
```

## Sending and Burning \(Retiring\) Credits

Sending and burning \(or retiring\) of credits is done via the `bank.Send` and `bank.Burn` transactions.

## Queries

```text
struct CreditHolding {
  liquidUnits: Decimal
  burnedUnits: Decimal
}

query GetCreditHolding(credit AssetID, holder: Address) CreditHolding
```

## State

```text
table CreditClass {
  id: uint64
  metadata: data.HashURI
  designer: Address
  issuers: Address*
  validationScript: script.ScriptID?
  @auto_primary_key(id)
  @index(designer)
  @multi_index(issuers)
}
```

