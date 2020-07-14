# lambdacli query distr slashes

## Description

Query all slashes of a validator for a given block range

## Usage:

```
 lambdacli query distr slashes <validator-address> <start-height> <end-height> [flags]
```

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for slashes                                             |
| --height       | Int    | False    |                       | Block height to query, omit to get most recent provable block|
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query distr slashes lambdavaloper1uhz9p4kcej80znwqcvr4v6rheg96ls0qg3m5q9 1 48800 -o json --indent
[
  {
    "validator_period": "6",
    "fraction": "0.000099953372134050"
  }
]
```
​           
