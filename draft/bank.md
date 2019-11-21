# Bank

## Assets

```text
scalar AssetID

struct Asset {
  asset: AssetID
  amount: Decimal
}
```

## Escrow Accounts

```text
enum Escrow {
  ContinuousVesting(
    start_time DateTime,
    end_time
  )
  DelayedVesting()
  PeriodicVesting()
  ScriptEscrow(scipt ScriptID, params bytes)
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

### Create Escrow

```text
tx CreateEscrow(
  escrow Escrow,
  initialFunds Asset*,
  parties EscrowParty*
)

type EscrowParty {
  party: Address,
  role: uint32
} 
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

table AssetBalance {
  address: Address
  asset: AssetID
  balance: Decimal
  burned: Decimal
  @primary_key(address, asset)
  @index(address)
  @index(asset)
}

table EscrowAccount {
  address: Address
  escrow: Escow
}

table EscrowParty {
  escrow_account: Address
  party: Address
  role: uint32
  @primary_key(escrow_account, party)
  @index(escrow_account)
  @index(party)
}
```

