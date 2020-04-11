# lambdacli tx market order-renewal

## Introduction

Send transaction to renewal a match order

## Usage

``
 lambdacli tx market order-renewal [orderId] [duration] [flags]
```

Print help messages:
```
lambdacli tx market order-renewal --help
```

## Unique Flags

| Name, shorthand              | type   | Required | Default  | Description                                                         |
| ---------------------------- | -----  | -------- | -------- | ------------------------------------------------------------------- | 
| --from                       | string | true     | ""       |  Name or address of private key with which to sign |

```
## Examples

```
lambdacli tx market order-renewal 6064A8751DE890DFC87A61F089A6911810B33AC2 1month --from user
```

Sample Output:
```txt
{"chain_id":"songtest","account_number":"3","sequence":"1","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgOrderRenewal","value":{"Address":"lambda16f32afm7zgayje7fzj477hqmcdkcwep6dwdlx7","OrderId":"6064A8751DE890DFC87A61F089A6911810B33AC2","duration":"2592000000000000"}}],"memo":""}

confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'zcTest':
Response:
  Height: 124
  TxHash: 055C73FDC9C7063724C02EC311B12306078244BB58EEA84D7A3A580BE3E81409
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 41720
  Tags: 
    - action = orderRenewal
    - address = lambda16f32afm7zgayje7fzj477hqmcdkcwep6dwdlx7
```

```json
 {
 	"height": "124",
 	"txhash": "055C73FDC9C7063724C02EC311B12306078244BB58EEA84D7A3A580BE3E81409",
 	"raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
 	"logs": [{
 		"msg_index": "0",
 		"success": true,
 		"log": ""
 	}],
 	"gas_wanted": "200000",
 	"gas_used": "41720",
 	"tags": [{
 		"key": "action",
 		"value": "orderRenewal"
 	}, {
 		"key": "address",
 		"value": "lambda16f32afm7zgayje7fzj477hqmcdkcwep6dwdlx7"
 	}],
 	"tx": {
 		"type": "auth/StdTx",
 		"value": {
 			"msg": [{
 				"type": "lambda/MsgOrderRenewal",
 				"value": {
 					"Address": "lambda16f32afm7zgayje7fzj477hqmcdkcwep6dwdlx7",
 					"OrderId": "6064A8751DE890DFC87A61F089A6911810B33AC2",
 					"duration": "2592000000000000"
 				}
 			}],
 			"fee": {
 				"amount": null,
 				"gas": "200000"
 			},
 			"signatures": [{
 				"pub_key": {
 					"type": "tendermint/PubKeySecp256k1",
 					"value": "AuIkUOBCfH//rPNoT+pDZ5YtULrKwX2a0P39GDEqJzkC"
 				},
 				"signature": "41W1u1YhaQrP1uZagDX8MyruNBZgE3WgwWLFu55OsudLy0ZKcPj7MncBDEpHubCxuG6y+1OWrL6cTWs6FCFPyQ=="
 			}],
 			"memo": ""
 		}
 	},
 	"timestamp": "2020-04-04T09:10:18Z"
 }
```
