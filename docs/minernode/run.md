# minernode run

## Description

Run miner service

## Usage
```
  minernode run [flags]
```
## Flags

| Name, shorthand| Default   | Description | Required                                                                  |
| --------------- | ----   | -------- | --------------------- 
| --daemonize    |  |run as daemon|
|  --debug   |   | run in debug mode|
|  --fees  |   | Fees to pay along with transaction; eg: 10ulamb|
|  --gas  |  200000 | gas limit to set per-transaction; set to "auto" to calculate required gas automatically|
|  --gas-prices  |   |Gas prices to determine the transaction fee (e.g. 1.0ulamb)|
|  --indent |   | Add indent to JSON response|
|  --ledger |   | Use a connected Ledger device|
| --kad.bootstrap_addr    | | kad bootstrap address|
|  --kad.external_address   |   | kad registered address(to other nodes)|
| --keepalive-interval   |  |run as daemon|
| --key-file   |   | private key file which associated to master miner account and to sign|
| --log.file    |  |log file path for daemon|
|  --log.level  |   | loglevel debug\|info\|warn\|error\|fatal (default "info")|
| --miner.ensure_level    |  | 0 : 1/6 of disk-space would be used for data-replicating	1 : 1/3 of disk-space would be used for data-replicating|
| --query-interva |  7 |  The miner query task interval(second), minimum query interval is 5s|
|  --restore |   false | restore true |
|   --p-mode |   |  profile runtime or background |
|  --profile |   false | restore true |
|  --miner.root_secret_seed   |   | root secret key for generate apikey|
| --node    | tcp://localhost:26657 |\<host\>:\<port\> to tendermint rpc interface for this chain |
|  --server.address   | 0.0.0.0:13000 | listen address )|
| --server.private_address    |172.11.159.11:13001 |private listen address |
|  --status  |   | get daemon status|
|  --stop  |   | stop daemon|


## Examples

Run miner service

```
./minernode run --daemonize --node tcp://182.91.242.11:26657 --trust-node --log.level debug --log.file /root/LambdaIM/storage/storage-feature_order_list_with_provider_status-984f41e-debug-03251653/minernode.log --kad.bootstrap_addr 182.91.242.11:13000 --server.address 172.11.159.11:14000 --server.private_address 172.11.159.11:14001 --kad.external_address 182.91.242.11:14000 --miner.root_secret_seed minernoderootsecretseedramdon --debug

```

get daemon status

```
./minernode run --status 
minernode.pid is running, pid is 24584
```

stop daemon

```
./minernode run --stop
stop daemon process from minernode.pid:24584 successfully
```
