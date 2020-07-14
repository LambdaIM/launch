# lambdacli query dam match-order

## Description

Query match order by order ID

## Usage:

```
 lambdacli query dam match-order [orderID] [flags]
```

`orderID`: order ID of the match order

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for match-order                                             |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query dam match-order 65F21496016CDF70F165E32FB9FC43B5B19B87CA
Dam MatchOrder
  OrderID:               65F21496016CDF70F165E32FB9FC43B5B19B87CA
  Asset:                 uabc
  BuyAddress:            lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
  AskAddress:            lambdamineroper10gat77jd5ucz7gw0m3xac8jfj5l83r6c0mswdj
  DhtID:                 5QCtxE1EhyanVkcv9v4mr3hhKDoUaZUYUrYJoTzrRd4r
  Price:                 3000000
  Size:                  100
  CreateTime:            2020-07-01 07:19:19.565201 +0000 UTC
  EndTime:               2020-07-31 07:19:19.565201 +0000 UTC
  WithDrawTime:          2020-07-01 07:19:19.565201 +0000 UTC
  UserPay:               300000000uabc
```

