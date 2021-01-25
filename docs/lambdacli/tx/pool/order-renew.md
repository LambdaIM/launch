# lambdacli tx pool order-renew

## Introduction

Send transaction to renew a pool match order

## Usage

```
 lambdacli tx pool order-renew [orderId] [duration] [flags]
```

Print help messages:
```
lambdacli tx pool order-renew --help
```

## Unique Flags

| Name, shorthand              | type   | Required | Default  | Description                                                         |
| ---------------------------- | -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from                       | string | true     | ""       |  Name or address of private key with which to sign |

```
## Examples

```
lambdacli tx pool order-renew 00E9FD13AABCA4CAEA0492C9938B970192A41A08 --from miner1
```

Sample Output:
```txt
{"chain_id":"test-chain-OU5P31","account_number":"2","sequence":"3","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgPoolOrderRenewal","value":{"address":"lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel","orderID":"00E9FD13AABCA4CAEA0492C9938B970192A41A08"}}],"memo":""}

confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'miner1':
Response:
  Height: 2913
  TxHash: B65C91E211F1ECBD769FC21257051D5C261B7504C5B73F89E8C2EFA39D9869ED
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 9794
  Tags:
    - action = poolOrderRenewal
    - address = lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel
    - endTime = 2021-03-23 07:21:32.6443 +0000 UTC
```