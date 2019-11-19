# Data

```text
module Data

scalar HashIRI

enum Datatype (
  Bool
  Integer
  Decimal
  String
  DateTime
  Date
  Time
  DateTimeInterval
  Duration
  Geography
)

enum Arity (
  One
  Ordered
  Unordered
)

tx CreateNamespace(name string) HashIRI

tx CreateClass(
  namespace HashIRI,
  name string,
  requiredProperties HashIRI*,
  superClasses HashIRI*
)

tx CreateDataProperty(
  namespace HashIRI,
  name string,
  datatype Datatype,
  arity Arity
)

tx CreateObjectProperty(
  namespace HashIRI,
  name string,
  cls HashIRI,
  arity Arity,
  superProperties HashIRI*
)

tx AnchorData(iri HashIRI)

tx SignData(iri HashIRI)

tx StoreGraph(data bytes)

tx RegisterDataURL(iri HashIRI, urls URL*)

tx StorePartialData(iri HashIRI, proofs ics23.ExistenceProof*)

table Namespace {
  iri: HashIRI
  owner: Address
  name: string
  @primary_key(iri)
  @unique(owner, name)
  @index(owner)
}

enum ObjType {
  DataProperty,
  ObjectProperty,
  Class
}

table Object {
  iri: HashIRI
  namespace: HashIRI
  name: string
  type: ObjType
  datatype: Datatype?
  cls: HashIRI?
  arity: Arity?
  super_properties: HashIRI*
  super_classes: HashIRI*
  required_properties: HashIRI*
  @primary_key(iri)
  @unique(namespace, name)
  @index(namespace)
}

table DataTimestamp {
  iri: HashIRI
  timestamp: DateTime
  @primary_key(iri)
}

table Data {
  iri: HashIRI
  data: bytes?
  partial: ics23.ExistenceProof*
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

## Transactions

### `AnchorData`

### `SignData`

### `StoreData`

### `RegisterDataURL`

### `StoreDataPartial`

