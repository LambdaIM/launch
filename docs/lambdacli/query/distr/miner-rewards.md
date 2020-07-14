# lambdacli query distr miner-rewards

## Description

Query miner rewards

## Usage:

```
 lambdacli query distr miner-rewards [miner] [flags]
```

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for miner-rewards                                             |
| --height       | Int    | False    |                       | Block height to query, omit to get most recent provable block|
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
First, use `lambdacli keys show m1 --bech miner` to get miner operator address
```
./lambdacli keys show m1 --bech miner
NAME:	TYPE:	ADDRESS:					PUBKEY:
m1	local	lambdamineroper14chzwvsh5y4yt489ea3vqelq3rpf6t8335k9jf	lambdamineroperpub1addwnpepqfel98pplh7zflh5937z52hfacy0zade9g2ch0ckyhhhfj0zvzl5wdw3kse
```
Use miner operator address to query:
```
./lambdacli query distr miner-rewards lambdamineroper14chzwvsh5y4yt489ea3vqelq3rpf6t8335k9jf
43783707.987450000000000000ulamb
```

​           
