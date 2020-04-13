# storagenode0.2.5 配置 
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

参考如下说明手动修改配置文件  
`vi ~/.lambda_storage/config/config.toml`

```
[build]
version = "0.2.5"
commit = "030c696bc6829cfafb3d240d66058b16b41aa460"
mode = "release"

# 服务需要监听的地址
# 以本机内网IP为 192.168.10.20，端口映射的外网IP为 200.200.200.200 为例
[server]
# 对外提供服务的地址，推荐配置为内网地址做端口映射到外网IP
address = "192.168.10.20:14000"
# 对内提供服务的地址，主要是给StorageNode使用，推荐配置为内网地址
private_address = "192.168.10.20:14001"

[kad]
# address you want kad to connect with
# DHT接入节点地址，可以是自己质押的验证节点或minernode配置的kad.external_address，这里以 47.94.129.97:13000 为例
# 可选官方dht地址：39.105.148.217:13000/47.94.129.97:13000/47.93.196.236:13000/182.92.66.63:13000
bootstrap_addr = ["47.94.129.97:13000"]
# time you would wait to connect dht seed node
db_path = "/root/.lambda_storage/kademlia"
# this should listen at Public IP
external_address = "200.200.200.200:14000"

[log]
level = "info"
output_file = "stdout"

[storage]
## 用于生成apikey的种子内容，不能为空
root_secret_seed = "fasdf"
## 存储节点的名字，需要在矿池内部唯一，即连接同一矿工的多个storagenode的storage_name不能重复
storage_name = "machine1"
## minernode对内提供服务的地址，即它的server.private_address
miner_address = "192.168.10.10:13001"
## 存储路径，可填写多个以逗号隔开
data_dir = ["/root/.lambda_storage"]

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

### 备份和恢复存储文件
以防配置文件丢失，请提前做好文件备份：[存储网络文件备份](StorageFile-Backup.md)



