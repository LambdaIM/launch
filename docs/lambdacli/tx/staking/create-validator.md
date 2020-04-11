# lambdacli tx staking create-validator

## Introduction

Send transaction to apply to be validator and delegate a certain amount tokens on it

For more detailed information, please refer to [Join Mainnet](../../join-mainnet.md)

## Usage

``
lambdacli tx staking create-validator [flags]
```

Print help messages:
```
lambdacli tx staking create-validator --help
```

## Unique Flags

| Name, shorthand              | type   | Required | Default  | Description                                                         |
| ---------------------------- | -----  | -------- | -------- | ------------------------------------------------------------------- |
| --amount                     | string | true     | ""       | Amount of coins to bond | 
| --details                    | string | false    | ""       | Optional details |
| --identity                   | string | false    | ""       | Optional identity signature (ex. UPort or Keybase) |
| --ip                         | string | false    | ""       | Node's public IP. It takes effect only when used in combination with |
| --moniker                    | string | true     | ""       | Validator name |
| --pubkey                     | string | true     | ""       | Go-Amino encoded hex PubKey of the validator. For Ed25519 the go-amino prepend hex is 1624de6220 |
| --website                    | string | false    | ""       | Optional website |

## Examples

```
lambdacli tx staking create-validator \
    --amount 666666666utbb \
    --broadcast-mode block \
    --from vestor1 \
    --moniker val2 \
    --pubkey lambdavalconspub1zcjduepq8qu9rg2srwxq9ze202pk6u8594e55mz909kuup3czr0mqvlfjjlslea3cn
```

Sample Output:
```txt
{"chain_id":"testing","account_number":"2","sequence":"0","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgCreateValidator","value":{"description":{"moniker":"val2","identity":"","website":"","details":""},"commission":{"rate":"0.250000000000000000","max_rate":"0.250000000000000000","max_change_rate":"0.010000000000000000"},"min_self_delegation":"666666666","delegator_address":"lambda188xynycq7hq94ftntmv99m3jltqt5tkk709uzn","validator_address":"lambdavaloper188xynycq7hq94ftntmv99m3jltqt5tkkgtvhc8","pubkey":"lambdavalconspub1zcjduepq8qu9rg2srwxq9ze202pk6u8594e55mz909kuup3czr0mqvlfjjlslea3cn","value":{"denom":"utbb","amount":"666666666"},"validator_type":1}}],"memo":""}

confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'vestor1':
Response:
  Height: 163
  TxHash: C0BB55729E27D3348D5D1FE127D989E35AAEBE2BFD526A5A8FF690B97DA71EDC
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 121363
  Tags:
    - action = create_validator
    - destination-validator = lambdavaloper188xynycq7hq94ftntmv99m3jltqt5tkkgtvhc8
    - moniker = val2
    - identity =
```

```json
 {
	"height": "163",
	"txhash": "C0BB55729E27D3348D5D1FE127D989E35AAEBE2BFD526A5A8FF690B97DA71EDC",
	"raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
	"logs": [{
		"msg_index": "0",
		"success": true,
		"log": ""
	}],
	"gas_wanted": "200000",
	"gas_used": "121363",
	"tags": [{
		"key": "action",
		"value": "create_validator"
	}, {
		"key": "destination-validator",
		"value": "lambdavaloper188xynycq7hq94ftntmv99m3jltqt5tkkgtvhc8"
	}, {
		"key": "moniker",
		"value": "val2"
	}, {
		"key": "identity"
	}],
	"tx": {
		"type": "auth/StdTx",
		"value": {
			"msg": [{
				"type": "lambda/MsgCreateValidator",
				"value": {
					"description": {
						"moniker": "val2",
						"identity": "",
						"website": "",
						"details": ""
					},
					"commission": {
						"rate": "0.250000000000000000",
						"max_rate": "0.250000000000000000",
						"max_change_rate": "0.010000000000000000"
					},
					"min_self_delegation": "666666666",
					"delegator_address": "lambda188xynycq7hq94ftntmv99m3jltqt5tkk709uzn",
					"validator_address": "lambdavaloper188xynycq7hq94ftntmv99m3jltqt5tkkgtvhc8",
					"pubkey": "lambdavalconspub1zcjduepq8qu9rg2srwxq9ze202pk6u8594e55mz909kuup3czr0mqvlfjjlslea3cn",
					"value": {
						"denom": "utbb",
						"amount": "666666666"
					},
					"validator_type": 1
				}
			}],
			"fee": {
				"amount": null,
				"gas": "200000"
			},
			"signatures": [{
				"pub_key": {
					"type": "tendermint/PubKeySecp256k1",
					"value": "AtbLEiwks5YXVnut8lhggFD+4tIYoyq/gTl2SfBS0afW"
				},
				"signature": "jQZI0cVgwmHgdSHo/juvaXxTBI0bILWzxBtueAOROXscsFb/+UEhDB3a9h0Zjy2phPUTWnqOaKTiFZQ4dfsHUQ=="
			}],
			"memo": ""
		}
	},
	"timestamp": "2019-08-23T07:04:56Z"
}
```
