# lambdacli query distr community-pool

## Description

Query all coins in the community pool which is under Governance control.

## Usage:

```
lambdacli query distr community-pool [flags]
```

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for community-pool                                             |
| --height       | Int    | False    |                       | Block height to query, omit to get most recent provable block|
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples

```
./lambdacli query distr community-pool 

output
7263141.324163332705670495ulamb
```

​           
