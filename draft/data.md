# Data

## Data Types

### `HashURI`

```text
scalar HashURI
```

* support [IPFS CID standard](https://docs.ipfs.io/guides/concepts/cid/)
* support [URDNA2015](https://json-ld.github.io/normalization/spec/) RDF graph normalization hashes
* DRGCA2019 \(Directed RDF Graph Canonicalization Algorithm 2019\): TODO

## Transactions

```text
tx AnchorData(iri HashURI)
```

### Registering URL's for Anchored Data

```text
tx RegisterDataURL(iri HashURI, urls URL*)
```

## Signing Data

```text
tx SignData(iri HashIRI)
```

## State

```
table DataTimestamp {
  iri: HashIRI
  timestamp: DateTime
  @primary_key(iri)
}

table DataURL {
  iri: HashIRI
  urs: URL
  @primary_key(iri, url)
}

table DataSigner {
  iri: HashIRI
  signer: Address
  timestamp: DateTime
  @primary_key(iri, signer)
}
```

