# lambdacli tx market create-market

## Introduction

Send transaction to create a market

## Usage

```
lambdacli tx market create-market [flags]
```

Print help messages:
```
lambdacli tx market create-market --help
```

## Unique Flags

| Name, shorthand              | type   | Required | Default  | Description                                                         |
| ---------------------------- | -----  | -------- | -------- | ------------------------------------------------------------------- |
| --name                       | string | true     | ""       | market name | 
| --profit                     | string | true     | ""       | get market income address |
| --fee-rate                   | string | true     | ""       | sell order fee rate by market |
| --commission-rate            | string | true     | ""       | match order commission rate by market |
| --from                       | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
 lambdacli tx market create-market --name xxx-market \
    --profit lambda1v7rq4afpf47wfq4qymyaa9mvvvq69f7f6k7cv9 \
    --fee-rate 0.02 \
    --commission-rate 0.02 --from master

```

Sample Output:
```txt
{"chain_id":"lambdatest","account_number":"0","sequence":"1","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgCreateMarket","value":{"name":"taobao","address":"lambda1v7rq4afpf47wfq4qymyaa9mvvvq69f7f6k7cv9","profit":"lambda1v7rq4afpf47wfq4qymyaa9mvvvq69f7f6k7cv9","feeRate":"0.020000000000000000","commissionRate":"0.020000000000000000"}}],"memo":""}

confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'master':
Response:
  Height: 5
  TxHash: A7322BE775C13D5974CCAEDEA9A630F42AEF6970876037B8F7F5C08051CA16D2
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 17447
  Tags: 
    - action = createMarket
    - address = lambda1v7rq4afpf47wfq4qymyaa9mvvvq69f7f6k7cv9

  Timestamp: 2019-10-29T03:13:44Z

```

```json
 {
 	"height": "5",
 	"txhash": "A7322BE775C13D5974CCAEDEA9A630F42AEF6970876037B8F7F5C08051CA16D2",
 	"raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
 	"logs": [{
 		"msg_index": "0",
 		"success": true,
 		"log": ""
 	}],
 	"gas_wanted": "200000",
 	"gas_used": "17447",
 	"tags": [{
 		"key": "action",
 		"value": "createMarket"
 	}, {
 		"key": "address",
 		"value": "lambda1v7rq4afpf47wfq4qymyaa9mvvvq69f7f6k7cv9"
 	}],
 	"tx": {
 		"type": "auth/StdTx",
 		"value": {
 			"msg": [{
 				"type": "lambda/MsgCreateMarket",
 				"value": {
 					"name": "taobao",
 					"address": "lambda1v7rq4afpf47wfq4qymyaa9mvvvq69f7f6k7cv9",
 					"profit": "lambda1v7rq4afpf47wfq4qymyaa9mvvvq69f7f6k7cv9",
 					"feeRate": "0.020000000000000000",
 					"commissionRate": "0.020000000000000000"
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
 				"signature": "2k13nrcaqNZOobu0upGXFK/vkAVPAx3K1D/qYMJhpxYmRyZBdFvrCEUgz74Z1Rro67x5Zj4pC4zybbrupVJcBg=="
 			}],
 			"memo": ""
 		}
 	},
 	"timestamp": "2019-10-29T03:13:44Z"
 }
```
