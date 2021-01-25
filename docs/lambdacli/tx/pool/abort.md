# lambdacli tx pool abort

## Introduction

Send transaction to abort tokens from the pool

## Usage

```
lambdacli tx pool abort [amount] [flags]
```

Print help messages:
```
lambdacli tx pool abort --help
```

## Unique Flags

| Name, shorthand              | type   | Required | Default  | Description                                                         |
| ---------------------------- | -----  | -------- | -------- | ------------------------------------------------------------------- | 
| --from                       | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
 $ ./lambdacli tx pool abort 10000000000ulamb --from user

```

Sample Output:
```txt
{"chain_id":"test-chain-OU5P31","account_number":"0","sequence":"1","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgSupplierAbort","value":{"address":"lambda1rf09ksku4t6u3qd8qp72ty67unpvxkwgnufv6t","marketName":"lambdax","amount":{"denom":"ulamb","amount":"10000000000"}}}],"memo":""}

confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'validator':
Response:
  Height: 2727
  TxHash: E966A7DA26F24D32499B762119E0A0BEEA14A61D70C65824EF6E591A297FF694
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 32549
  Tags:
    - action = supplierAbort
    - address = lambda1rf09ksku4t6u3qd8qp72ty67unpvxkwgnufv6t
    - amount = 10000000000ulamb
```