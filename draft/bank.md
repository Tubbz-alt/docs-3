# Bank

## Assets

```
scalar AssetID

struct Asset {
  asset: AssetID
  amount: Decimal
}
```

## Transactions

### Send

```
tx Send(
  from Address,
  to Address,
  assets Asset*
)
```

### Burn

```
tx Burn(
  holder Address,
  assets Asset*
)
```

## Queries

```
query GetBalance(address Address, asset Asset) Decimal
```

## State

```
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

