# lambdacli query dam asset-match-orders

## Description

Query all delegations to one digital asset miner by asset

## Usage:

```
 lambdacli query dam asset-delegations-to [minerAddr] [asset] [flags]
```

- `minerAddress`: digital asset miner's address
- `asset`: asset name

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for asset-match-orders                    |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query dam asset-delegations-to lambdamineroper10gat77jd5ucz7gw0m3xac8jfj5l83r6c0mswdj uabc
Dam Delegation:
  Delegator: lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
  Miner:     lambdamineroper10gat77jd5ucz7gw0m3xac8jfj5l83r6c0mswdj
  Asset:     uabc
  Amount:    1000000000
```

