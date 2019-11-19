# Group

## Transactions

### Create Group

```text
tx CreateGroup(
  members: Member*
  metadata data.HashIRI?
) GroupID

type Member {
  account: Address
  weight: Decimal
  metadata: data.HashIRI?
}

util AssetGroupID(asset AssetID) GroupID
```

### Create Group Account

```text
tx CreateGroupAccount(
  group GroupID,
  decisionPolicy DecisionPolicy,
  metadata data.HashIRI?
) Address
```

## Exec

```text
tx GroupAccountExec(
  groupAccount Address,
  actions Tx*
)
```

### Proposals

#### Create

```text
tx CreateProposal(
  groupAccount Address,
  actions Tx*
) ProposalID
```

#### ExecProposal

```text
tx ExecProposal(
  proposal ProposalID,
  choice uint8,
  comment data.HashIRI?
)  
```

## State

```text
table GroupMetadata {
  id: uint64
  metadata: data.HashIRI?
  admin: Address
  total_weight: Decimal
  @auto_primary_key(id)
  @index(admin)
}

table GroupMember {
  group: Address
  member: Address
  weight: Decimal
  @primary_key(group, member)
  @index(group)
  @index(member)
}

table GroupAccount {
  address: Address
  group: GroupID
  admin: Address
  decision_policy: DecisionPolicy
  @primary_key(address)
  @index(group)
  @index(admin)
}
```

