# lambdacli keys create-miner

## Description

Create an raw private key(json formatted), it used for miners to run miner-node server

## Usage

```
lambdacli keys create-miner <name> [flags]
```

## Flags

## Flags

| Name, shorthand | Default   | Description                                                  | Required |
| --------------- | --------- | ------------------------------------------------------------ | -------- |
| --help, -h      |           | help for create-miner                                              |          |
| --output-dir    |           | Set the output dir to detrive private key file (default ".") | false |

## Examples

### Create a new key

```shell
lambdacli keys create-miner miner
```

You'll be asked to enter bip39 mnemonic for your master account. The miner account will be associated to master account

```txt
Enter your bip39 mnemonic:
```

After that, you're done with creating a miner account key. The generated key file will looks like below:

```json
{
  "pub_key": {
    "type": "tendermint/PubKeySecp256k1",
    "value": "A8yMo684pcg6rSFzIlBF/G+ZzuElC7TdjGLeetlcNljW"
  },
  "priv_key": {
    "type": "tendermint/PrivKeySecp256k1",
    "value": "5abzq1fW527qsowb1oaFflfz1KL4xk0386z8853DnM8="
  },
  "masterAddress": "lambda1zevzfj7h7pee633gguckcq5keca6pnyztlsvrx",
  "address": "lambda1e7l6f8j0rl7z0fgptlgsjdnhdjm2xcmy8p7ce9"
}
```

Then move this key file to your mining device to start minernode service
