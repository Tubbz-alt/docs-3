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

#### CreateProposal

```text
tx CreateProposal(
  groupAccount Address,
  actions Tx*,
  metadata *data.HashIRI?
) ProposalID
```

#### Vote

```text
tx Vote(
  proposal ProposalID,
  choice uint8,
  comment data.HashIRI?
)
```

#### ExecProposal

```text
tx ExecProposal(proposal ProposalID)
```

## Asset Distribution

```text
// Distributes the provides assets to all the members of the group
// proportionally to their weight
tx DistributeAssets(group GroupID, assets Asset*)
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

table Proposal {
  id: uint64
  group_account: Address
  actions: Tx*
  start_time: DateTime
  end_time: DateTime?
  metadata: data.HashIRI?
  @auto_primary_key(id)
  @index(group_account)
}

table Vote {
  proposal: ProposalID
  voter: Address
  vote: uint8
  metadata: data.HashIRI?
  @primary_key(proposal, voter)
  @index(proposal)
  @index(voter)
}
```

