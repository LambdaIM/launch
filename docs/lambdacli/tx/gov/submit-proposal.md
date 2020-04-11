# lambdacli tx submit a text proposal

## Introduction

Submit a text proposal
## Usage

```
lambdacli tx gov submit-proposal text <path/to/proposal.json> --from peter

Where proposal.json contains:

{
  "title": "Test Proposal",
  "description": "My awesome proposal",
  "deposit": [
    {
      "denom": "ulamb",
      "amount": "10000"
    }
  ]
}
```

Print help messages:
```
lambdacli tx gov submit-proposal text --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx gov submit-proposal text proposal.json --from peter
```

Output:

```
Response:
  Height: 6497
  TxHash: 2FD19442DBCBA6F343F7098CDA1B53C491929E0ADC6849C6175CE978CB47D5EA
  Data: 0101
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 68922
  Tags:
    - action = submit_proposal
    - sender = lambda1mn7dvaa45mzfefq52antavyvfjluvsgl3v3pyw
    - proposal_id = 1
```

# lambdacli tx submit a community pool spend proposal

## Introduction

Submit a community pool spend proposal

## Usage

```
lambdacli tx gov submit-proposal community-pool-spend <path/to/proposal.json> --from peter

Where proposal.json contains:

{
  "title": "Community Pool Spend",
  "description": "Pay me some lamb!",
  "recipient": "lamb1s5afhd6gxevu37mkqcvvsj8qeylhn0rz46zdlq",
  "amount": [
    {
      "denom": "ulamb",
      "amount": "10000"
    }
  ],
  "deposit": [
    {
      "denom": "ulamb",
      "amount": "10000"
    }
  ]
}
```

Print help messages:
```
lambdacli tx gov submit-proposal community-pool-spend --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx gov submit-proposal community-pool-spend proposal.json --from peter
```

Output:

```
Response:
  Height: 6497
  TxHash: 2FD19442DBCBA6F343F7098CDA1B53C491929E0ADC6849C6175CE978CB47D5EA
  Data: 0101
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 68922
  Tags:
    - action = submit_proposal
    - sender = lambda1mn7dvaa45mzfefq52antavyvfjluvsgl3v3pyw
    - proposal_id = 1
```

# lambdacli tx submit a parameter change proposal

## Introduction

Submit a parameter change proposal

## Usage
```
lambdacli tx gov submit-proposal param-change <path/to/proposal.json> --from peter

Where proposal.json contains:


{
  "title": "Staking Param Change",
  "description": "Update max validators",
  "changes": [
    {
      "subspace": "staking",
      "key": "MaxValidators",
      "value": 105
    }
  ],
  "deposit": [
    {
      "denom": "ulamb",
      "amount": "10000"
    }
  ]
}
```

Print help messages:
```
lambdacli tx gov submit-proposal param-change --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx gov submit-proposal param-change proposal.json --from peter
```

Output:

```
Response:
  Height: 6497
  TxHash: 2FD19442DBCBA6F343F7098CDA1B53C491929E0ADC6849C6175CE978CB47D5EA
  Data: 0101
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 68922
  Tags:
    - action = submit_proposal
    - sender = lambda1mn7dvaa45mzfefq52antavyvfjluvsgl3v3pyw
    - proposal_id = 1
```

# lambdacli tx submit a burn coins proposal

## Introduction

Submit a burn coins proposal

## Usage
```
lambdacli tx gov submit-proposal burn-coins <path/to/proposal.json> --from peter

Where proposal.json contains:


{
  "title": "Burn coins",
  "description": "Burn some coins!",
  "burn_amount": [
    {
      "denom": "ulamb",
      "amount": "10000"
    }
  ],
  "deposit": [
    {
      "denom": "ulamb",
      "amount": "10000"
    }
  ]
}
```

Print help messages:
```
lambdacli tx gov submit-proposal burn-coins --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx gov submit-proposal burn-coins proposal.json --from peter
```

Output:

```
Response:
  Height: 6497
  TxHash: 2FD19442DBCBA6F343F7098CDA1B53C491929E0ADC6849C6175CE978CB47D5EA
  Data: 0101
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 68922
  Tags:
    - action = submit_proposal
    - sender = lambda1mn7dvaa45mzfefq52antavyvfjluvsgl3v3pyw
    - proposal_id = 1
```
