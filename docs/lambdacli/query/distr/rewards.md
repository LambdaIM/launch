# lambdacli query distr rewards

## Description

Query all rewards earned by a delegator, optionally restrict to rewards from a single validator

## Usage:

```
 lambdacli query distr rewards [delegator-addr] [<validator-addr>] [flags]
```

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for rewards                                             |
| --height       | Int    | False    |                       | Block height to query, omit to get most recent provable block|
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples

```
lambdacli query distr rewards lambda12ege5pja3mrzaz6dcwueqw737a8lnyke2ypec7 lambdavaloper1h7pnxzejqtzlfcad89hkn0ersjqmfsj8n8s6vy

output
7376.769964095849500000ulamb
```

​           
