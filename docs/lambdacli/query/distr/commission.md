# lambdacli query distr commission

## Description

Query validator commission rewards from delegators to that validator

## Usage:

```
 lambdacli query distr commission <validator-address> [flags]
```

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for commission                                             |
| --height       | Int    | False    |                       | Block height to query, omit to get most recent provable block|
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples

```
 lambdacli query distr commission lambdavaloper1v7rq4afpf47wfq4qymyaa9mvvvq69f7fvjhnk3
 
 output:
 32281423.265160217982593431ulamb
```

​           
