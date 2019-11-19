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


```

## Transactions

### `AnchorData`

### `SignData`

### `StoreData`

### `RegisterDataURL`

### `StoreDataPartial`

