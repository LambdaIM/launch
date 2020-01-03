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
After initializing "storagenode", a default configuration file ~ / .lamborage / config / node.toml is generated, and then modified: node.toml


```

[server]
# Binding Addresses required for service startup
# Intranet network address, which can be mapped to "kad.external_address" port, please choose the port by yourself，you may start with 0.0.0.0，such as 0.0.0.0:13000
address = ""  

[kad]
# DHT seed node address provided by lambda network
bootstrap_addr = "39.105.148.217:13000"  ## Optional DHT address：39.105.148.217:13000/47.94.129.97:13000/47.93.196.236:13000
# Public network address, which can be mapped to "server.address" port, please choose the 
port by yourself
external_address = ""

[gateway]
# Store the binding address required for the gateway service to start, ./storagenode gateway starts to use this address
# Internal network address, which can be mapped to the "gateway.external_address" port, please choose the port by yourself，you may start with 0.0.0.0, such as 0.0.0.0:9000
address = ""
# Public network address, which can be mapped to "gateway.address" port, please choose the port
external_address = "" 
# gateway configuration file directory
conf_dir = "/root/.lamborage/gateway"
# Data storage directory, you can configure multiple paths such as ["/root/.lamborage/store","/root/.lamborage/newstore"]
data_dir = ["/root/.lamborage/store"]
# Mining data storage address, multiple paths can be configured such as ["/root/.lamborage/store/mining","/root/.lamborage/newstore/mining"]
mining_dir = ["/root/.lamborage/store/mining"]

[message]
# storage_name is the name of the storagenode "machine-name";
storage_name = "machine-name" 
# MINER REST address
# Connect the rest service started by the miner node. Both the internal network and the public IP can be used. For example, miner-server and storagenode can write the internal IP in the same internal network.
miner_address = "" 
```

### Start-Storagenode

Start storagenode server and storagenode gateway。
```
./storagenode server --daemonize --log.file storage-server.log
./storagenode gateway --daemonize  --debug --log.file storage-gateway.log
```
  
Explanation:
--daemonize start in background mode;  
--log.file storage-server.log output to the current directory "storage-server.log" file, can be modified to other directories and no log output without adding parameters;    
Add --debug parameter to "storagenode gateway" startup mode to [test the storagenode service](./Testnet0.4.0-Miner-guide-en.md#3Storagenode-Connection-Test);    

You can add the "--log.level debug" parameter. If you enable debugging, you can view more detailed log output. If you do not add this parameter, the INFO log is output by default. 


### Storagenode Status
```
./storagenode server --status
```
```
If the return value is as follows, the program runs normally:
storagenode_server.pid is running, pid is 21058
```
```
./storagenode gateway --status
```
```
If the return value is as follows, the program runs normally:
storagenode_gateway.pid is running, pid is 19985
```


### Storagenode Stop
If you need to stop "storagenode server / gateway", please refer to the following command


```
./storagenode server --stop
```
```
If the return value is as follows, the cease was successful:
stop daemon process from storagenode_server.pid:21058 successfully
```
```
./storagenode gateway --stop
```
```
If the return value is as follows, the cease was successful:
stop daemon process from storagenode_gateway.pid:19985 successfully
```


