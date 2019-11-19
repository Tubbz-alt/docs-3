# Bank

```text
module Bank

scalar AssetID

type Asset {
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
```

