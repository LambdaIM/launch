# lambdacli tx pool declare-mining

## Introduction

Send transaction to declare mining to the pool

## Usage

```
lambdacli tx pool declare-mining [flags]
```

Print help messages:
```
lambdacli tx pool declare-mining --help
```

## Unique Flags

| Name, shorthand              | type   | Required | Default  | Description                                                         |
| ---------------------------- | -----  | -------- | -------- | ------------------------------------------------------------------- | 
| --from                       | string | true     | ""       |  Name or address of private key with which to sign |
| --size                       | string | true     | ""       |  The amount of space to declare mining |

## Examples

```
 $ ./lambdacli tx pool declare-mining --size 100GB --from miner1

```

Sample Output:
```txt
{"chain_id":"test-chain-OU5P31","account_number":"2","sequence":"0","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgDeclareMining","value":{"address":"lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel","marketName":"lambdax","size":"100"}}],"memo":""}

confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'miner1':
Response:
  Height: 2760
  TxHash: E2388C61C7B48D01F4F63D519E9D17D08DD3AEAB7B8F2EB4E8F3A3779AA99643
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 43761
  Tags:
    - action = declareMining
    - address = lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel
    - marketName = lambdax
    - matchOrderID = 00E9FD13AABCA4CAEA0492C9938B970192A41A08
    - matchOrder = 0a28303045394644313341414243413443414541303439324339393338423937303139324134314130381214d376e492894516a4e099b6f9e1a811a3fac685c01a14d376e492894516a4e099b6f9e1a811a3fac685c03a03313030420c08fcf9a9800610e0f99cb3024a0c08fc93c8810610e0f99cb3025a0c08fcf9a9800610e0f99cb3026a1427cac5503836765cd10751d27ab4a6e17d7a80d4720a0a05756c616d621201307a0a0a05756c616d62120130
    - fee = 900000ulamb
    - endTime = 2021-02-21 07:21:32.6443 +0000 UTC
```