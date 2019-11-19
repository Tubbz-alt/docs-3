# Bank

## Transactions

```text

```

```text
module Bank

scalar AssetID

struct Asset {
  asset: AssetID
  amount: Decimal
}

tx Send(
  from Address,
  to Address,
  assets Asset*
)

tx Burn(
  holder Address,
  assets Asset*
)

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

