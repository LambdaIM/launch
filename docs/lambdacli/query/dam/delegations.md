# lambdacli query dam delegations

## Description

Query user's all delegations made by one delegator

## Usage:

```
lambdacli query dam delegations [address] [flags]
```

- `address`: delegator's address

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for asset-match-orders                    |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query dam delegations lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
Dam Delegation:
  Delegator: lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
  Miner:     lambdamineroper10gat77jd5ucz7gw0m3xac8jfj5l83r6c0mswdj
  Asset:     uabc
  Amount:    1000000000
```

