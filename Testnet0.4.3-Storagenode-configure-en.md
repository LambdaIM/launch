# Storagenode Deployment
* [Storagenode Initialization](#Storagenode-Initialization)
* [Modify Configuration](#Modify-Configuration)
* [Start Storagenode](#Start-Storagenode)


### Storagenode-Initialization

If the create storage node is initialized, ignore this step

```
./storagenode init 
```

### Modify-Configuration
After initializing "storagenode", a default configuration file `~/.lambda_storage/config/config.toml` is generated, and then modified: config.toml


```
# Binding Addresses required for service startup
# For example when intranet IP is 192.168.10.20，public IP 200.200.200.200 
[server]
# Binding Addresses required for service startup
# Intranet network address, which can be mapped to "kad.external_address" port, please choose the port by yourself
address = "192.168.10.20:14000"
# Intranet network address
private_address = "192.168.10.20:14001"
debug_log_traffic = "false" 

[kad]
# DHT seed node address provided by lambda, multiple addresses can be configured
# Optional DHT address：39.105.148.217:13000/47.94.129.97:13000/47.93.196.236:13000/182.92.66.63:13000
bootstrap_addr = ["47.94.129.97:13000"]
# time you would wait to connect dht seed node
bootstrap_backoff_max = "30s"
bootstrap_backoff_base = "1s"
db_path = "/root/.lambda_storage/kademlia"
# this should listen at Public IP
external_address = "200.200.200.200:14000"
alpha = 3

[kad.routing_table_config]
bucket_size = 20
replacement_cache_size = 5

[log]
level = "info"
output_file = "stdout"

[storage]
## used to create root apikey, cannot be null
root_secret_seed = "fasdf"
## Data storage directory, you can configure multiple paths
data_dir = [ "/root/.lambda_storage/store"]
## Connect the rest service started by the miner node, be same to server.private_address in miner config 
miner_address = "192.168.10.10:13001"
## storagenode name, need to be unique below one miner
storage_name = "machine1"

[mining]
## Statement data
db_path = "/root/.lambda_storage/statementdb"
## Mining data storage address, multiple paths can be configured
mining_dir = [ "/root/.lambda_storage/mining"]

```

### Start-Storagenode

Start storagenode
```
./storagenode run --daemonize --log.file [log_file_path]
```
  
Explanation:
--daemonize start in background mode;  
--log.file storage-server.log output to the current directory "storage-server.log" file, can be modified to other directories and no log output without adding parameters;    
 

You can add the "--log.level debug" parameter. If you enable debugging, you can view more detailed log output. If you do not add this parameter, the INFO log is output by default. 


### Storagenode Status
```
./storagenode run --status
```
```
If the return value is as follows, the program runs normally:
storagenode.pid is running, pid is 19505
```

### Storagenode Stop
If you need to stop "storagenode", please refer to the following command


```
./storagenode run  --stop
```
```
If the return value is as follows, the cease was successful:
stop daemon process from storagenode.pid:19505 successfully
```



