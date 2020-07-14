# lambdacli tx market edit-market

## Introduction

Send transaction to edit a market

## Usage

```
lambdacli tx market edit-market [flags]
```

Print help messages:
```
lambdacli tx market edit-market --help
```

## Unique Flags

| Name, shorthand   | type   | Required | Default  | Description                                                         |
| ----------------- | -----  | -------- | -------- | ------------------------------------------------------------------- | 
| --profit          | string | false    | ""       | get market income address |
| --fee-rate        | string | false    | ""       | sell order fee rate by market |
| --commission-rate | string | false    | ""       | match order commission rate by market |
| --order-price | string | false    | ""       | market min order price can be modify (default "[do-not-input-value]") |
| --from            | string | true     | ""       | Name or address of private key with which to sign |

## Examples

```
 lambdacli tx market edit-market --commission-rate 0.01 --from master

```

Sample Output:
```txt
{"chain_id":"lambdatest","account_number":"0","sequence":"2","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgEditMarket","value":{"address":"lambda1v7rq4afpf47wfq4qymyaa9mvvvq69f7f6k7cv9","profit":"","feeRate":null,"commissionRate":"0.010000000000000000"}}],"memo":""}

confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'master':
Response:
  Height: 102
  TxHash: 3EB9438642D7ABBAC6A6920D109141FEC717341629A547E0823B4B8DD9BD75CC
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 17293
  Tags: 
    - action = editMarket
    - address = lambda1v7rq4afpf47wfq4qymyaa9mvvvq69f7f6k7cv9
    - commissionRate = 0.010000000000000000

  Timestamp: 2019-10-29T03:21:57Z

```

```json
 {
 	"height": "102",
 	"txhash": "3EB9438642D7ABBAC6A6920D109141FEC717341629A547E0823B4B8DD9BD75CC",
 	"raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
 	"logs": [{
 		"msg_index": "0",
 		"success": true,
 		"log": ""
 	}],
 	"gas_wanted": "200000",
 	"gas_used": "17293",
 	"tags": [{
 		"key": "action",
 		"value": "editMarket"
 	}, {
 		"key": "address",
 		"value": "lambda1v7rq4afpf47wfq4qymyaa9mvvvq69f7f6k7cv9"
 	}, {
 		"key": "commissionRate",
 		"value": "0.010000000000000000"
 	}],
 	"tx": {
 		"type": "auth/StdTx",
 		"value": {
 			"msg": [{
 				"type": "lambda/MsgEditMarket",
 				"value": {
 					"address": "lambda1v7rq4afpf47wfq4qymyaa9mvvvq69f7f6k7cv9",
 					"profit": "",
 					"feeRate": null,
 					"commissionRate": "0.010000000000000000"
 				}
 			}],
 			"fee": {
 				"amount": null,
 				"gas": "200000"
 			},
 			"signatures": [{
 				"pub_key": {
 					"type": "tendermint/PubKeySecp256k1",
 					"value": "A8wLxTD30uOdHNvAal9ZFdUzhBY5rOjr7LG9r1GkEtzX"
 				},
 				"signature": "3IK+LvDnzJY5Y+lJn920ASf4LSsnVo1tjyK5FuOv3o5nDjyjLj6TofbumqG13JcfPbsyap7b0ENkk1NPbTUoLg=="
 			}],
 			"memo": ""
 		}
 	},
 	"timestamp": "2019-10-29T03:21:57Z"
 }
```
