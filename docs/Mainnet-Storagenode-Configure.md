# storagenode0.2.7.3 配置 

**注意**  
存储接入前需要先同步当前服务器时间到最新时间
``` 
ntpdate -u ntp.api.bz
```
如服务器上无`ntpdate`命令，可使用`sudo yum install -y ntpdate`(CentOS)或`sudo apt-get install ntpdate -y`(Ubuntu)进行安装

### 1. storagenode初始化

如果存储节点已初始化，请忽略此步骤

```
./storagenode init
```

### 2. 修改配置文件
初始化`storagenode`后，默认生成配置文件`~/.lambda_storage/config/config.toml`

!!! abstract ""
    
    === "修改存储节点配置"  
    
        1. 配置存储节点对外提供服务的地址（以存储节点所在机器的外网IP为 200.200.200.200为例）：
        ```
        ./storagenode config kad.external_address 200.200.200.200:14000
        ```
        2. 配置存储节点连接矿工服务（以minernode对内提供服务的地址即它的server.private_address为例）：
        ```
        ./storagenode config storage.miner_address 192.168.10.10:13001
        ```
        
        3. 修改文件存储路径（默认路径为`/root/.lambda_storage`，以修改为多个磁盘路径/data1/test和/data2/test为例）
        ```
        ./storagenode config storage.data_dir /data1/test,/data2/test
        ```
        
        4. (可选)修改metadb存储路径（默认路径为`/root/.lambda_storage/meta`，以修改为/data1/test/meta为例）
        ```
        ./storagenode config storage.meta_dir /data1/test/meta
        ```
        
        ??? note "展开查看配置说明"
            ```shell hl_lines="27 39 41"
            [build]
            version = "0.2.7.3"
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
            # DHT接入节点地址，可以是自己质押的验证节点或minernode配置的kad.external_address
            bootstrap_addr = [
                      "zjk.mainnet.lambdastorage.com:12000",
                      "hhht.mainnet.lambdastorage.com:12000",
                      "bj.mainnet.lambdastorage.com:12000",
                      "hk.mainnet.lambdastorage.com:12000",
                      "tokyo1.mainnet.lambdastorage.com:12000",
                      "tokyo2.mainnet.lambdastorage.com:12000",]
    
            db_path = "/root/.lambda_storage/kademlia"
            # this should listen at Public IP
            external_address = "200.200.200.200:14000"
            
            [log]
            level = "info"
            output_file = "stdout"
            
            [storage]
            ## 用于生成apikey的种子内容，不能为空
            root_secret_seed = "fasdf"
            ## 存储节点名称，需在矿池内部唯一，即连接同一矿工的多个storagenode的storage_name不能重复。存储节点启动后，请勿修改此名称
            storage_name = "machine1"
            ## minernode对内提供服务的地址，即它的server.private_address
            miner_address = "192.168.10.10:13001"
            ## 存储路径，可填写多个以逗号隔开
            data_dir = ["/root/.lambda_storage"]
            
            ```

### 3. 启动storagenode

启动storagenode
```
./storagenode run --daemonize --log.file [log_file_path]
```
说明：  
```
--daemonize以后台方式启动   
--log.file [log_file_path] 指定storagenode运行日志路径，不添加参数则无日志输出  
可添加--log.level debug参数，日志开启debug可查看更详细日志输出，不添加此参数则默认输出INFO级别日志 
```


#### 3.1 查询声明状态
使用`storagenode mining status`查询当前声明数量及提交状态，加上`--with-resolved`参数查询结果包含已提交成功的声明。
``` 
./storagenode mining status --with-resolved
```
查询结果说明：
```
Page size: 100
Current block time: 2020-05-14 05:52:56 UTC

Pending setups  # 等待提交的声明，Retry为该声明重复提交的次数

# |Setup |Retry |LastRetry


Resolving setups  # 已经提交的声明


# |Setup |Retry |LastRetry


Resolved setups  # 提交成功的声明

#    |Setup                                |Expiry                  |Expired |FinalExpiry             |X
0001 |b3aef44e-2a99-4fb7-b313-ad2b5b0f473d |2020-05-24 04:30:47 UTC |        |2020-06-13 04:12:37 UTC |0
```

#### 3.2 查看storagenode进程
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



