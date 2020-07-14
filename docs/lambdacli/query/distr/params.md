# lambdacli query distr params

## Description

query chain distribution params

## Usage:

```
 lambdacli query distr params [flags]
```

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for params                                             |
| --height       | Int    | False    |                       | Block height to query, omit to get most recent provable block|
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples

```
./lambdacli query distr params
 Distribution Params:
   Community Tax:          "0.020000000000000000"
   Base Proposer Reward:   "0.010000000000000000"
   Bonus Proposer Reward:  "0.040000000000000000"
   Withdraw Addr Enabled:  true
```

​           
