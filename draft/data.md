# Data

## Schema

### HashURI

```text
scalar HashURI
```

* Multihash
  * ex: SHA-256, Blake2b-256
* URDNA2015
* DRGCA2019 \(Directed RDF Graph Canonicalization Algorithm 2019\)

### Datatypes

```text
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
```

### Namespaces

```text
tx CreateNamespace(name string) HashURI
```

### Properties

#### Data Properties

```text
tx CreateDataProperty(
  namespace HashURI,
  name string,
  datatype Datatype,
  arity Arity
)
```

#### Object Properties

```text
tx CreateObjectProperty(
  namespace HashURI,
  name string,
  cls HashIRI,
  arity Arity,
  superProperties HashURI*
)
```

#### Arity

```text
enum Arity (
  One,
  Ordered,
  Unordered
)
```

### Classes

```text
tx CreateClass(
  namespace HashURI,
  name string,
  requiredProperties HashURI*,
  superClasses HashURI*
)
```

## Anchoring Data

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

## Storing Graph Data

```go
tx StoreGraph(data bytes) HashURI
```

### Storing Part of a Graph

```text
tx StorePartialData(iri HashIRI, proofs ics23.ExistenceProof*)
```

### Deleting Data

```text
// this would allow the person who committed data to remove it from state
// but not from transaction history - maybe no point in even considering this
@experimental tx DeleteData(iri HashIRI)
```

## State

```text
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

