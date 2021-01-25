# lambdacli tx pool mining-withdraw

## Introduction

Send transaction to withdraw mining reward

## Usage

```
lambdacli tx pool mining-withdraw [flags]
```

Print help messages:
```
lambdacli tx pool mining-withdraw --help
```

## Unique Flags

| Name, shorthand              | type   | Required | Default  | Description                                                         |
| ---------------------------- | -----  | -------- | -------- | ------------------------------------------------------------------- | 
| --from                       | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
 $ ./lambdacli tx pool mining-withdraw --from miner1

```

Sample Output:
```txt
{"chain_id":"test-chain-OU5P31","account_number":"2","sequence":"2","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgLoaneeWithDraw","value":{"address":"lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel","marketName":"lambdax"}}],"memo":""}

confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'miner1':
Response:
  Height: 2873
  TxHash: 2E727045D4FD51FC5D584886B03F3EFE633050D55F89E53076CD95A61E345191
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 14282
  Tags:
    - action = loaneeWithdraw
    - address = lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel
    - marketName = lambdax
    - reward = 1000ulamb
```