# lambdacli tx pool withdraw

## Introduction

Send transaction to withdraw supply reward

## Usage

```
lambdacli tx pool withdraw [flags]
```

Print help messages:
```
lambdacli tx pool withdraw --help
```

## Unique Flags

| Name, shorthand              | type   | Required | Default  | Description                                                         |
| ---------------------------- | -----  | -------- | -------- | ------------------------------------------------------------------- | 
| --from                       | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
 $ ./lambdacli tx pool withdraw --from user

```

Sample Output:
```txt
{"chain_id":"test-chain-OU5P31","account_number":"0","sequence":"2","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgSupplierWithdraw","value":{"address":"lambda1rf09ksku4t6u3qd8qp72ty67unpvxkwgnufv6t","marketName":"lambdax"}}],"memo":""}

confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'validator':
Response:
  Height: 2888
  TxHash: ED8A5795C0569ABD2266B6E22C484320D386DFA55EB4DA1F7FCFD011216B8932
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 13384
  Tags:
    - action = supplierWithdraw
    - address = lambda1rf09ksku4t6u3qd8qp72ty67unpvxkwgnufv6t
    - reward = 100ulamb
```