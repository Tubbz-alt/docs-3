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

## Queries

```text
query GetBalance(address Address, asset AssetID) Decimal
query GetSupply(asset AssetID) Decimal
query GetBurnedSupply(asset AssetID) Decimal)
```

## State

```text
table AssetMetadata {
  asset: AssetID
  authority: bytes
  module: bytes
  name: string
  metadata: data.HashIRI?
  @primary_key(asset)
}

table AssetSupply {
  asset: AssetID
  liquid_supply: Decimal
  burned_supply: Decimal
  @primary_key(asset)
}

interface Holding

table AssetHolding {
  address: Address
  asset: AssetID
  holding: Holding
  @primary_key(address, asset)
  @index(address)
  @index(asset)
}
```

