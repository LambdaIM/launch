# Commands of lambda

## Global Flags

| Name, shorthand | Default        | Description                            | Required |
| --------------- | -------------- | -------------------------------------- | -------- |
| --encoding, -e  | hex            | Binary encoding (hex\b64\btc) |          |
| --home          | $HOME/.lambda    | Directory for config and data |          |
| --output, -o    | text           | Output format (text\json)     |          |
| --trace         |                | Print out full stack trace on errors   |          |

## Available Commands

Name, shorthand | Description 
:- | :- 
init | Initialize genesis and node's configuration files 
collect-gentxs | Collect genesis txs and output a genesis.json file
testnet | Initialize files for a Lambda testnet
gentx | Generate a genesis tx carrying a self delegation
validate-genesis | Validates the genesis file at the default location or at the location passed as an arg
start | Run the full node
unsafe-reset-all | Resets the blockchain database, removes addr_book and resets priv_validator.json
tendermint | Tendermint subcommands
export | Export state to JSON
version | Print the app version
service | view lambda service status

## init

### Description

Initialize genesis and node's configuration files 

### Usage

```bash
./lambda init [moniker] --chain-id [chain-id]
```  

**tips**
if left chain-id blank, it will be randomly created

## collect-gentxs

### Description

Collect genesis txs and output a genesis.json file. 

### Usage

```bash
./lambda collect-gentxs
```

This command is available after gentx, you can set --gentx-dir to override default gentx path to collect gentxs

## testnet

### Description

Initialize files for a Lambda testnet 

### Usage

```bash
./lambda testnet
```

### Flags

Name, shorthand | Default | Description | Required
:- | :- | :- | :-
--chain-id | | genesis file chain-id, if left blank will be randomly created | 
--minimum-gas-prices | 0.000006ulamb | Minimum gas prices to accept for transactions |
--node-cli-home | lambdacli | Home directory of the node's cli configuration |
--node-daemon-home | lambda | Home directory of the node's daemon configuration |
--node-dir-prefix | node | Prefix the directory name for each node with |
-o, --output-dir | ./mytestnet | Directory to store initialization data for the testnet |
--starting-ip-address | 192.168.0.1 | Starting IP address |
--v | 4 | Number of validators to initialize the testnet with |

## gentx

### Description

Generate a genesis tx carrying a self delegation 

### Usage

```bash
./lambda gentx --name [name]
```

### Flags

Name, shorthand | Default | Description | Required
:- | :- | :- | :-
--amount | 666666666utbb | Amount of coins to bond |
--commission-max-change-rate | 0.010000000000000000 | The maximum commission change rate percentage (per day) |
--commission-max-rate | 0.200000000000000000 | The maximum commission rate percentage | 
--commission-rate | 0.100000000000000000 | The initial commission rate percentage | 
--details | | The validator's (optional) details | 
--home-client | $Home/.lambdacli | Directory to store initialization data for the testnet | 
--identity | | The (optional) identity signature | 
--ip | 192.168.1.20 | The node's public IP | 
--min-self-delegation | 666666666utbb | The minimum self delegation required on the validator |
--name | | name of private key with which to sign the gentx | true
--node-id | | The node's NodeID | 
--output-document | | write the genesis transaction JSON document to the given file instead of the default location | 
--pubkey | | The Bech32 encoded PubKey of the validator | 
--website | | The validator's (optional) website | 

## add-genesis-account

### Description

Add genesis account to genesis.json

### Usage

```bash
./lambda add-genesis-account [address_or_key_name] [coin][,[coin]]
```

### Flags

Name, shorthand | Default | Description | Required
:- | :- | :- | :-
--home-client | $Home/.lambdacli | client's home directory | 
--vesting-amount | | amount of coins for vesting accounts |
--vesting-end-time | | schedule end time (unix epoch) for vesting accounts | 
--vesting-start-time | | schedule start time (unix epoch) for vesting accounts | 

## start

### Description

Run the full node

### Usage

```bash
./lambda start
```

### Flags

Name, shorthand | Default | Description | Required
:- | :- | :- | :-
--abci | socket | Specify abci transport (socket | grpc) | 
--address | tcp://0.0.0.0:26658 | Listen address |
--consensus.create_empty_blocks | true | Set this to false to only produce blocks when there are txs or when the AppHash changes | 
--fast_sync | true | Fast blockchain syncing | 
--moniker | | Node Name | 
--p2p.laddr | tcp://0.0.0.0:26656 | Node listen address | 
--p2p.persistent_peers | | Comma-delimited ID@host:port persistent peers | 
--p2p.pex | true | Enable/disable Peer-Exchange | 
--p2p.private_peer_ids | | Comma-delimited private peer IDs | 
--p2p.seed_mode | false | Enable/disable seed mode | 
--p2p.upnp | | Enable/disable UPNP port forwarding | 
--priv_validator_laddr | | Socket address to listen on for connections from external priv_validator process | 
--proxy_app | tcp://127.0.0.1:26658 | Proxy app address | 
--pruning | syncable | Pruning strategy: syncable, nothing, everything | 
--replay-last-block | | Replay the last block | 
--rpc.grpc_laddr | | GRPC listen address (BroadcastTx only). Port required | 
--rpc.laddr | tcp://0.0.0.0:26657 | RPC listen address. Port required | 
--rpc.unsafe | false | Enabled unsafe rpc methods | 
--trace-store | | Enable KVStore tracing to an output file | 
--with-tendermint | true | Run abci app embedded in-process with tendermint | 

## reset 

### Description

Reset app state to the specified height

### Usage

```bash
./lambda reset --height [height]
```

## unsafe-reset-all

### Description

Resets the blockchain database, removes address book files, and resets priv_validator.json to the genesis state

### Usage

```bash
./lambda unsafe-reset-all
```

## tendermint

### Description

Tendermint subcommands

### Usage

```bash
./lambda tendermint show-node-id
```
Show this node's ID

```bash
./lambda tendermint show-validator
```
Show this node's tendermint validator info

```bash
./lambda tendermint show-address
```
Shows this node's tendermint validator consensus address

```bash
./lambda tendermint version
```
Print tendermint libraries' version

## export

### Description

Export state to JSON

### Usage

```bash
./lambda export --for-zero-height --height [height]
```

### Flags

Name, shorthand | Default | Description | Required
:- | :- | :- | :-
--for-zero-height | | Export state to start at height zero (perform preproccessing) | 
--height | -1 | Export state from a particular height (-1 means latest height) |
--vesting-end-time | | schedule end time (unix epoch) for vesting accounts | 
--jail-whitelist | | List of validators to not jail state export | 

## version

### Description

Print the app version

### Usage

```bash
./lambda version --long
```

## service

### Description

View lambda service status

### List

```bash
./lambda service list
```

list all lambda service status

### Show

```bash
./lambda service show [name]
```

show the designated service status

## key

### Description

Key allows users to backup or recover local validator consensus private key

### Backup

```bash
./lambda key backup --method [qr|text] --key-path [backup key path]
```

backup provides 2 ways to backup node's consensus private key, user can set `--method qr` or `--method text` and `--key-path` to a given backup path.

### Recover

```bash
./lambda key recover --method [qr|text|seeds] --key-path [backup key path]
```

recover provides 3 ways to recover node's consensus private key locally. If user set `--method seeds`, you need to input the seeds displayed when init the node. Otherwise, you can recover by a given text file or qr image file.

## upgrade

### Description

Upgrade allows to upgrade lambda configurations to newest

### Usage 

```bash
./lambda upgrade 
```

First check if configs and other files need to upgrade. If necessary, it will upgrade automatically