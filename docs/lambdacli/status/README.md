# lambdacli status

## Description

Query remote node for status

## Usage

```shell
lambdacli status <flags>
```

## Flags

| Name, shorthand       | Default               | Description                         | Required |
| --------------------- | --------------------- | ----------------------------------- | -------- |
| --help, -h            |                       | Help for status                     |          |
| --node, -n            | tcp://localhost:26657 |\<host>:\<port> to tendermint rpc interface for this chain |          |

## Examples

### Query remote node for status

```shell
lambdacli status --indent
```

After that, you can get remote node status as follows:

```json
{
  "node_info": {
    "protocol_version": {
      "p2p": "7",
      "block": "10",
      "app": "0"
    },
    "id": "e02882af5bdafa5aec086c32b8398c268d2337f1",
    "listen_addr": "47.93.196.236:26656",
    "network": "lambda-chain-test4.8",
    "version": "0.4.8-goleveldb",
    "channels": "4020212223303800",
    "moniker": "cv-moniker-1",
    "other": {
      "tx_index": "on",
      "rpc_address": "tcp://0.0.0.0:26657"
    }
  },
  "sync_info": {
    "latest_block_hash": "9F42CA967AC4E245A4481B514F3EBB972E94A29E2BF948949096874DB4BB16E4",
    "latest_app_hash": "8F06E082FF105161346098F4EAA6863A433A3763B1CC28EF55211FC57A212B05",
    "latest_block_height": "49871",
    "latest_block_time": "2020-04-15T06:57:20.032158835Z",
    "catching_up": false
  },
  "validator_info": {
    "address": "3B4F49BD7E16BE11EFC841ED672FCE3643B1F688",
    "pub_key": {
      "type": "tendermint/PubKeyEd25519",
      "value": "a6X7p6CBEnzN76j0UXGSQ++bgNN59yyzE/X3LDgrssU="
    },
    "voting_power": "1749"
  }
}
```
