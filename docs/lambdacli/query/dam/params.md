# lambdacli query dam params

## Description

query chain dam params

## Usage:

```
 lambdacli query dam params [flags]
```

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for params                                |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples

```
./lambdacli query dam params
Params:
  min_pledge_space:             1
  max_name_length:              32
  create_market_cost            1000000000000
  pub_key_type:                 [ed25519]
  jailed_duration:              1440h0m0s
  refunding_duration:	        504h0m0s
  max_file_length:              256
  min_order_price:              1000000
  order_price_time:             2592000000000000
  order_min_buy_duration:       720h0m0s
  order_max_buy_duration:       43200h0m0s
  order_with_draw_min_duration: 24h0m0s
  miner_with_draw_duration:     1h0m0s
```

​           
