# lambdacli query asset params

## Description

query asset params

## Usage:

```
 lambdacli query asset params [flags]
```

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for params                                             |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples

```
./lambdacli query asset params
Params:
  asset_prefix:    u
  pledge_cost:     1000000000000
  max_name_length: 32
  max_supply:      90000000000000000
  issue_cost_rate: 0.100000000000000000
  exclude_symbols: [lamb tbb 1amb]
```

​           
