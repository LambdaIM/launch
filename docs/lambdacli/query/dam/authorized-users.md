# lambdacli query dam authorized-users

## Description

Query authorized users by asset

## Usage:

```
lambdacli query dam authorized-users [asset] [page] [limit] [flags]
```

- `asset`: asset name
- `page`: page of authorized users
- `limit`: max authorized users per page 

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for all-match-orders                                             |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query dam authorized-users uabc 1 100
lambda1vw5a7mykczyxzhreh9ddeqxpg7ffdks43ldqj4
lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel
```

