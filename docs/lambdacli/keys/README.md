# lambdacli keys

## Description

Keys allows you to manage your local keystore for tendermint.

## Usage

```shell
lambdacli keys <command>
```

## Available Commands

| Name                    | Description                                                                                  |
| ----------------------- | -------------------------------|
| [mnemonic](mnemonic.md) | Create a bip39 mnemonic, sometimes called a seed phrase, by reading from the system entropy. |
| [add](add.md)           |  Add an encrypted private key (either newly generated or recovered), encrypt it, and save to disk. | 
| [list](list.md)         | List all keys                                                                                |
| [show](show.md)         | Show key info for the given name                                                             |
| [delete](delete.md)     | Delete the given key                                                                         |
| [update](update.md)     | Change the password used to protect private key                                              |
| [create-miner](create_miner.md)     | Create an raw private key(json formatted), it used for miners to run miner-node server.|
| [pubkey-file](pubkey-file.md)     | Get public key file from private key file                       |
| [repair](repair.md)     | repair keys db                       |

## Flags

| Name, shorthand | Default | Description   | Required |
| --------------- | ------- | ------------- | -------- |
| --help, -h      |         | Help for keys |          |

## Global Flags

| Name, shorthand | Default        | Description                            | Required |
| --------------- | -------------- | -------------------------------------- | -------- |
| --chain-id string | tendermint   | Chain ID of tendermint node |          |
| --encoding, -e  | hex            | Binary encoding (hex/b64/btc) |          |
| --home          | $HOME/.lambdacli | Directory for config and data |          |
| --output, -o    | text           | Output format (text/json)     |          |
| --trace         |                | Print out full stack trace on errors   |          |

## Extended description

These keys may be in any format supported by go-crypto and can be used by light-clients, full nodes, or any other application that needs to sign with a private key.
