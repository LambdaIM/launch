# lambdacli query dam pledge-records

## Description

Query all pledge records by address

## Usage:

```
 lambdacli query dam pledge-records [address] [flags]
```

- `address`: pledge records of the address

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for pledge-records                                             |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query dam pledge-records lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
DigitalAssetRecord
  assetName:           uabc
  orderPrice:          3000000
  power:               0
  miningSize:          1000.000000000000000000
  matchSize:           100.000000000000000000
  pledgeAsset:         10000000
  lastRewardHeight:    0
  selfChallengeHeight: 0
  available:           true
```

