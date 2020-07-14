# lambdacli keys pubkey-file

## Description

Get public key file from private key file for convenience

## Usage

```
lambdacli keys pubkey-file <name> <keyFilePath> [flags]
```

## Flags

| Name, shorthand | Default   | Description                                                  | Required |
| --------------- | --------- | ------------------------------------------------------------ | -------- |
| --help, -h      |           | help for pubkey-file                                              |          |
| --output-dir    |           | Set the output dir to detrive public key file (default ".") | false |

## Examples

### Get a public key file

```shell
lambdacli keys pubkey-file miner ./priv_key_file.json

output:
Public key file is generated at ./miner_pub_key.json
```

You could use this key file for authorizing asset mining in digital asset market or sharing it with statement buyers

