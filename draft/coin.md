# Coin

```text
tx CreateCoinAsset(minter Address, metadata data.HashURI) AssetID
tx UpdateMinter(asset AssetID, newMinter Address)
tx UpdateMetadata(asset AssetID, metadata data.HashURI)
tx MintCoins(asset AssetID, units Decimal, to Address)
```

