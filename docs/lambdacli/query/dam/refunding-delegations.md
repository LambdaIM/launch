# lambdacli query dam refunding-delegations

## Description

Query all refunding delegations made by delegator

## Usage:

```
lambdacli query dam refunding-delegations [address] [flags]
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
./lambdacli query dam refunding-delegations lambda17mzpym4zvtmlk8ulcrw77k5ty3jjcjupsuka89
Refunding Delegations between:
  Delegator:                 lambda17mzpym4zvtmlk8ulcrw77k5ty3jjcjupsuka89
  Miner:                     lambdamineroper10gat77jd5ucz7gw0m3xac8jfj5l83r6c0mswdj
  Asset:                     uabc
	Records:
	Refunding Record 0:
          Complete Time:             2020-09-08 03:12:14.50142 +0000 UTC
          Cost:                      1000000
	Refunding Record 1:
          Complete Time:             2020-09-08 03:19:28.434391 +0000 UTC
          Cost:                      100
```

