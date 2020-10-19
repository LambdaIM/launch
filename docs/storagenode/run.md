# storagenode run

## Description

Run storage service

## Usage

```
storagenode run [flags]
```
## Flags

| Name, shorthand| Default   | Description | Required                                                                  |
| --------------- | ----   | -------- | --------------------- 
| --daemonize  |  | run as daemon |
| --debug  |  | run in debug mode |
| --gateway.goroutine_count  |  | storagenode gateway goroutine count |
| --kad.bootstrap_addr  |  | kad bootstrap address |
| --kad.external_address  |  | kad registered address(to other nodes) |
| --log.file  |  | log file path for daemon |
| --log.level  | info | loglevel debug\|info\|warn\|error\|fatal |
| --log.output_file  | stdout | output file of log |
| --p-mode |  | profile mod |
| --profile |  |  profile runtime or background |
| --server.address  | 0.0.0.0:14000 | listen address |
| --server.private_address  | 172.11.159.11:14001 | private listen address |
| --status  | | get daemon status |
| --stop  |  | stop daemon |
| --storage.data_dir   | /root/.lambda_storage | dirs for storage and mining |
| --storage.keepalive_interval  | 5s | local keepalive interval to miner node |
| --storage.meta_dir   | /root/.lambda_storage/meta | dir for meta files |
| --storage.miner_address  |  | minernode address |
| --storage.order_cache_refresh_interval | 5m0s | local order cached refresh interval |
| --storage.root_secret_seed  |  | root secret key for generate apikey |
| --storage.setup_expire_check_batch  | 110 | check expired setup count every interval  |
| --storage.setup_pending_retry_batch  | 88 | retry pending setup count every interval  |
| --storage.setup_pending_retry_threshold  | 60 | retry pending setup maximum times  |
| --storage.setup_resolve_batch  | 88 | resolve setup count every interval |
| --storage.space_to_setup  |  | total space(GB) for mining, if set will ignore/overwrite storage.setup flags |
| --storage.storage_name  |  | storage name to represent current node |


## Examples
```
 run as daemon：
./storagenode run --daemonize --log.level debug --log.file /root/LambdaIM/storage/storage-feature_order_list_with_provider_status-984f41e-debug-03251653/storagenode.log --kad.bootstrap_addr 182.91.242.11:13000 --server.address 172.11.159.11:15000 --server.private_address 172.11.159.11:15001 --kad.external_address 182.91.242.11:15000 --storage.root_secret_seed storagenoderootsecretseedramdon --storage.storage_name t4s5 --storage.miner_address 172.11.159.11:14001 --debug

get daemon status：
./storagenode run --status  
storagenode.pid is running, pid is 16479

 stop daemon：
./storagenode run --stop 
stop daemon process from storagenode.pid:16479 successfully
```
