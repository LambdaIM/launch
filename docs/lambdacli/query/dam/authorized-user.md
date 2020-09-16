# lambdacli query dam authorized-user

## Description

Query authorized info by address asset

## Usage:

```
lambdacli query dam authorized-user [address] [asset] [flags]
```

- `address`: user's address
- `asset`: asset name

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help     |        | False    |                       | help for all-match-orders                                             |
| --ledger       | String | False    |                       | Use a connected Ledger device                                |
| --node         | String | False    | tcp://localhost:26657 | `<host>:<port>`to tendermint rpc interface for this chain    |
| --trust-node   | String | False    | True                  | Don't verify proofs for responses                            |


## Examples
```
./lambdacli query dam authorized-user lambda1vw5a7mykczyxzhreh9ddeqxpg7ffdks43ldqj4 uabc
AuthorizedUserResult
  user:           lambda1vw5a7mykczyxzhreh9ddeqxpg7ffdks43ldqj4
  isAuthorized:   true
```

