# lambdacli query dam transfer-file-record

## Description

Query transfer files by orderID and receiver's address

## Usage:

```
 lambdacli query dam transfer-file-record [orderID] [addr] [start] [end] [flags]
```

- `orderID`: order ID of the match order
- `addr`: address to receive transfer files related to the match order
- `start`: start index of transfered files
- `end`: end index of transferd files

**tips**

query result is a closure result by start and end if end is less than file numbers

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for transfer-file-record                                             |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query dam transfer-file-record 65F21496016CDF70F165E32FB9FC43B5B19B87CA  lambda1vw5a7mykczyxzhreh9ddeqxpg7ffdks43ldqj4 0 4
TransferFileRecordResult
  orderInfo:
  orderID:           65F21496016CDF70F165E32FB9FC43B5B19B87CA
  endTime:           2020-07-31 07:19:19.565201 +0000 UTC
  expired:           false

  files:   [bucketName/fileName bucketName/fileName1 bucketName/fileName2]
```

