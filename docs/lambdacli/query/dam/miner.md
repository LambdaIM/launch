# lambdacli query dam miner

## Description

Query digital asset miner by address

## Usage:

```
 lambdacli query dam miner [address] [flags]
```

- `address`: miner info of the address

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for miner                                             |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query dam miner lambdamineroper105jf3p5qkrnq973xmc6e9f8asly79sv74c5y3x
DigitalAssetMiner
  address:            lambdamineroper10gat77jd5ucz7gw0m3xac8jfj5l83r6c0mswdj
  totalSize:          100000.000000000000000000
  assetSet:
  [
  DigitalAssetRecord
  assetName:           uabc
  orderPrice:          3000000
  power:               10
  miningSize:          100000.000000000000000000
  matchSize:           100.000000000000000000
  pledgeAsset:         1000000000
  selfPledgeAsset:     1000000000

  ]
  jailedRecords:
  [

  ]
```

