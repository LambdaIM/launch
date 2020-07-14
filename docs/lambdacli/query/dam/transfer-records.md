# lambdacli query dam transfer-records

## Description

Query all transfer records by order ID

## Usage:

```
 lambdacli query dam transfer-records [orderID] [flags]
```

- `orderID`: order ID of the match order

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for transfer-records                                             |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query dam transfer-records 65F21496016CDF70F165E32FB9FC43B5B19B87CA
TransferRecordsResult
  orderInfo:
  orderID:           65F21496016CDF70F165E32FB9FC43B5B19B87CA
  endTime:           2020-07-31 07:19:19.565201 +0000 UTC
  expired:           false

  results:
  [
  receiver:          lambda1vw5a7mykczyxzhreh9ddeqxpg7ffdks43ldqj4
  fileNum:           3

  receiver:          lambda1d93vleu5x42u5jv25amqg4e73hsnmhxhp3wznd
  fileNum:           1
  ]
```

