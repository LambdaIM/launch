# storagecli gateway run

## Description

run local gateway --account [account] --debug

## Usage
```
 storagecli gateway run [flags]
```
## Flags

| Name, shorthand| Default   | Description | Required                                                                  |
| --------------- | ----   | -------- | --------------------- 
|--account   |  | specify account to use |
|--broker.db_path   |  | local gateway data directory |
|--broker.dht_gateway_addr   |  | remote dht gateway address |
|--broker.extra_key_file  |  | local path of extra key file |
|--broker.extra_order_id   |  | local gateway extra order id |
|--broker.validator_addr   |  | remote validator address |
|--debug  |  | enable debug log output |
|--gateway.access_key | accesskey | local gateway access key |
|--gateway.address   |  | local gateway address |
|--gateway.secret_key   | secretkey | local gateway secret key|
|--daemonize            |           | run as daemon|
|--log.file             |           | log file path for daemon|
|--status               |           |  get daemon status|
|--stop                 |           |  stop daemon|




## Examples

```
run as daemon:
./storagecli gateway run --account testu --broker.extra_order_id 0A0250B4143BD1F69DFBEBD98ADDDFEF99397511  --broker.dht_gateway_addr 182.91.242.11:13000 --broker.validator_addr 182.91.242.11:13659 --gateway.access_key lambda --gateway.secret_key 12345678 --log.file gateway.log --debug --daemonize

get daemon status:
./storagecli gateway run --account testu --broker.extra_order_id 0A0250B4143BD1F69DFBEBD98ADDDFEF99397511 --status
gateway.pid is running, pid is 22879

stop daemon:
./storagecli gateway run --account testu --broker.extra_order_id 0A0250B4143BD1F69DFBEBD98ADDDFEF99397511 --stop
stop daemon process from gateway.pid:22879 successfully

```
