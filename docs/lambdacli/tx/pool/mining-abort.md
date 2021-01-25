# lambdacli tx pool mining-abort

## Introduction

Send transaction to abort mining from the pool

## Usage

```
lambdacli tx pool mining-abort [flags]
```

Print help messages:
```
lambdacli tx pool mining-abort --help
```

## Unique Flags

| Name, shorthand              | type   | Required | Default  | Description                                                         |
| ---------------------------- | -----  | -------- | -------- | ------------------------------------------------------------------- | 
| --from                       | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
 $ ./lambdacli tx pool mining-abort 00E9FD13AABCA4CAEA0492C9938B970192A41A08 --from miner1

```

Sample Output:
```txt
{"chain_id":"test-chain-OU5P31","account_number":"2","sequence":"1","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgAbortMining","value":{"address":"lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel","orderID":"00E9FD13AABCA4CAEA0492C9938B970192A41A08"}}],"memo":""}

confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'miner1':
Response:
  Height: 2780
  TxHash: E2388C61C7B48D01F4F63D519E9D17D08DD3AEAB7B8F2EB4E8F3A3779AA99643
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 43761
  Tags:
    - action = abortMining
    - address = lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel
    - matchOrderID = 00E9FD13AABCA4CAEA0492C9938B970192A41A08
```