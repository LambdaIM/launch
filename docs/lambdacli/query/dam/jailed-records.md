# lambdacli query dam jailed-records

## Description

Query all jailed records by address

## Usage:

```
 lambdacli query dam jailed-records [address] [flags]
```

- `address`: jailed records related to this address

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for jailed-records                                             |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query dam jailed-records lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
JailedRecordResult
  assetName:          uabc
  endTime:            2020-08-15 09:12:19.575851 +0000 UTC
  unjailed:           false
```

