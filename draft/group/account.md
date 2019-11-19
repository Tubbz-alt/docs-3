# Account

```text
table Account {
  address: Address
  pubkey: PubKey
  metadata: data.HashIRI?
  @primary_key(address)
}

interface PubKey
```

