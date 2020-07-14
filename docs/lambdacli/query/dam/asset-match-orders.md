# lambdacli query dam asset-match-orders

## Description

Query all match orders related to the given asset by address

## Usage:

```
 lambdacli query dam asset-match-orders [address] [asset] [page] [limit] [flags]
```

- `address`: buyer's or pledge owner's address
- `asset`: match orders related to asset
- `page`: page of match orders
- `limit`: max match orders per page

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for asset-match-orders                    |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query dam asset-match-orders lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0 uabc 1 10
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

