# lambdacli query dam refunding-records

## Description

Query all refunding records by address

## Usage:

```
 lambdacli query dam refunding-records [address] [flags]
```

- `address`: refunding records of the address

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for refunding-records                                             |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query dam refunding-records lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
RefundingRecordResult
  assetName:            uabc
  creationHeight:       1466
  completionTime:       2020-07-07 09:12:19.575851 +0000 UTC
  Cost:                 10000000
```

