# lambdacli query txs

## Introduction

Search for transactions that match the exact given tags where results are paginated

[all msg type](txs_set.md)

## Usage

```
lambdacli query txs <flags>
```

Print query block flags:
```
lambdacli query block --help
```

## flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help       |        | false     |                       |  Help for txs                                        |
| --limit       |  uint32      | false     |     30                  |  Query number of transactions results per page returned (default 30)                                        |
| --page       |   uint32     | false     |       1                |  Query a specific page of paginated results (default 1)                                        |
| --tags       |    string    | true     |                       |  tag:value list of tags that must match                                       |

## Examples
```$xslt
lambdacli query txs --tags action:send --limit 1
```

output

```json
[{
	"height": "405",
	"txhash": "7E189FAF57262723FF0A1933EAB74A47F72916433DAD034775F8C474350A6960",
	"raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
	"logs": [{
		"msg_index": "0",
		"success": true,
		"log": ""
	}],
	"gas_wanted": "200000",
	"gas_used": "25416",
	"tags": [{
		"key": "action",
		"value": "send"
	}, {
		"key": "sender",
		"value": "lambda1v7rq4afpf47wfq4qymyaa9mvvvq69f7f6k7cv9"
	}, {
		"key": "recipient",
		"value": "lambda18fyevgyegm0mxrtylh8udpcw7pw6rvwk4zv020"
	}],
	"tx": {
		"type": "auth/StdTx",
		"value": {
			"msg": [{
				"type": "cosmos-sdk/MsgSend",
				"value": {
					"from_address": "lambda1v7rq4afpf47wfq4qymyaa9mvvvq69f7f6k7cv9",
					"to_address": "lambda18fyevgyegm0mxrtylh8udpcw7pw6rvwk4zv020",
					"amount": [{
						"denom": "ulamb",
						"amount": "1"
					}]
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
				"signature": "KmnPKc4cJ4idRDECzwN5FiP+SQgYsgNiYcsChi00XKc/XWpZW+TuKMm6Qc7fu6HX/ZLJHsYAtYlN+S99T8N8HA=="
			}],
			"memo": ""
		}
	},
	"timestamp": "2019-08-20T07:14:19Z"
}]
```

