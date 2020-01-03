# 配置 storagenode 
* [storagenode初始化](#storagenode初始化)
* [修改配置文件](#修改配置文件)
* [启动storagenode](#启动storagenode)


### storagenode初始化

如果存储节点已初始化，请忽略此步骤

```
./storagenode init 
```

### 修改配置文件
初始化storagenode后，默认生成配置文件~/.lambda_storage/config/config.toml


```
# 服务需要监听的地址
# 以本机内网IP为 192.168.10.20，端口映射的外网IP为 200.200.200.200 为例
[server]
# 对外提供服务的地址，推荐配置为内网地址做端口映射到外网IP
address = "192.168.10.20:14000"
# 对内提供服务的地址，主要是给StorageNode使用，推荐配置为内网地址
private_address = "192.168.10.20:14001"
debug_log_traffic = "false"


[kad]
# address you want kad to connect with
# DHT接入节点地址，可以是存储网络提供的地址，也可以是minernode暴露到外网的IP，这里以 47.94.129.97:13000 为例
# 可选dht地址：39.105.148.217:13000/47.94.129.97:13000/47.93.196.236:13000/182.92.66.63:13000
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
## 用于生成apikey的种子内容，不能为空
root_secret_seed = "fasdf"
## 存储路径，可填写多个以逗号隔开
data_dir = [ "/root/.lambda_storage/store"]
## minernode对内提供服务的地址，即它的server.private_address
miner_address = "192.168.10.10:13001"
## 存储节点的名字，需要在矿池内部唯一，即连接同一矿工的多个storagenode的storage_name不能重复
storage_name = "machine1"

[mining]
## 挖矿记录的数据文件
db_path = "/root/.lambda_storage/statementdb"
## 存储挖矿文件(删除的)的存储路径，可填写多个以逗号隔开
mining_dir = [ "/root/.lambda_storage/mining"]
```

### 启动storagenode

启动storagenode
```
./storagenode run --daemonize --log.file [log_file_path]
```
说明：  
--daemonize以后台方式启动   
--log.file [log_file_path] 指定storagenode运行日志路径，不添加参数则无日志输出  

可添加--log.level debug参数，日志开启debug可查看更详细日志输出，不添加此参数则默认输出INFO级别日志 


### 查看storagenode进程
```
./storagenode run --status
```
```
返回结果如下即为正常运行：
storagenode.pid is running, pid is 19505
```


### 停止storagenode

```
./storagenode run --stop
```
```
返回结果如下即停止成功：
stop daemon process from storagenode.pid:19505 successfully
```



