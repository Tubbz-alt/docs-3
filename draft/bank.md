# Bank

## Assets

```text
scalar AssetID

struct Asset {
  asset: AssetID
  amount: Decimal
}
```

## Transactions

### Send

```text
tx Send(
  from Address,
  to Address,
  assets Asset*
)
```

### Burn

```text
tx Burn(
  holder Address,
  assets Asset*
)
```

## State

```text
table AssetMetadata {
  asset: AssetID
  authority: bytes
  module: bytes
  name: string
  @primary_key(asset)
}

interface HoldingAccount

table Holding {
  address: Address
  asset: AssetID
  holding_account: HoldingAccount
  @primary_key(address, asset)
  @index(address)
  @index(asset)
}
```

