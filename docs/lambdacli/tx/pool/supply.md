# lambdacli tx pool supply

## Introduction

Send transaction to supply tokens to the pool

## Usage

```
lambdacli tx pool supply [amount] [flags]
```

Print help messages:
```
lambdacli tx pool supply --help
```

## Unique Flags

| Name, shorthand              | type   | Required | Default  | Description                                                         |
| ---------------------------- | -----  | -------- | -------- | ------------------------------------------------------------------- | 
| --from                       | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
 $ ./lambdacli tx pool supply 10000000000ulamb --from user

```

Sample Output:
```txt
{"chain_id":"test-chain-OU5P31","account_number":"0","sequence":"0","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgSupply","value":{"address":"lambda1rf09ksku4t6u3qd8qp72ty67unpvxkwgnufv6t","name":"lambdax","amount":{"denom":"ulamb","amount":"10000000000"}}}],"memo":""}

confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'validator':
Response:
  Height: 2657
  TxHash: FA44F77DEA54ECBF468ECBDAAB2AD0DB4B220C3875A371F073D917BE24B3A671
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 35070
  Tags:
    - action = supply
    - address = lambda1rf09ksku4t6u3qd8qp72ty67unpvxkwgnufv6t
    - amount = 10000000000ulamb
```