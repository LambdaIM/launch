# lambdacli query dam transfer-record

## Description

Query transfer record and file number by order ID and receiver's address

## Usage:

```
 lambdacli query dam transfer-record [orderID] [addr] [flags]
```

- `orderID`: order ID of the match order
- `addr`: address to receive transfer files related to the match order

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for transfer-record                                             |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query dam transfer-record  65F21496016CDF70F165E32FB9FC43B5B19B87CA  lambda1vw5a7mykczyxzhreh9ddeqxpg7ffdks43ldqj4
TransferRecordResult
  orderInfo:
  orderID:           65F21496016CDF70F165E32FB9FC43B5B19B87CA
  endTime:           2020-07-31 07:19:19.565201 +0000 UTC
  expired:           false

  result:
  receiver:          lambda1vw5a7mykczyxzhreh9ddeqxpg7ffdks43ldqj4
  fileNum:           3
```

