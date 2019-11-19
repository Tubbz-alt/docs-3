# Bank

```text
module Bank

scalar AssetID

tx Send(
  asset AssetID,
  from Address,
  to Address,
  amount Decimal
)

tx Burn(
  asset AssetID,
  holder Address,
  amount Decimal
)
```

