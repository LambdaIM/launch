# 主网Validator 0.5.1 升级教程

### 1. 下载安装包并解压
`创建目录并进入`
```
mkdir -p ~/LambdaIM && cd ~/LambdaIM  
```
如已有~/LambdaIM目录则直接进入目录：`cd ~/LambdaIM` 

`下载安装包`
```
wget https://github.com/LambdaIM/launch/releases/download/v0.5.1/lambda-0.5.1-release.tar.gz

如下载缓慢可使用下面的链接：
wget http://download.lambdastorage.com/lambda/0.5.1/lambda-0.5.1-release.tar.gz
```

`解压安装包`
```
tar zxvf lambda-0.5.1-release.tar.gz && cd lambda-0.5.1-release
```
### 2. 停止节点服务

```
kill `ps aux | grep lambda |grep -v grep| awk '{print $2}'`
```
备注：如果无法停止，请使用`ps aux|grep lambda`命令查看进程号，然后 `kill 进程号`

### 3. 清除旧版数据
```
./lambda unsafe-reset-all
```
```
rm ~/.lambda/config/addrbook.json
```

**注意**

不要删除~/.lambda/config下的`priv_validator_key.json`和`node_key.json`文件，
如果丢失会导致节点无法再正常加入共识网络，请节点注意备份

[备份和恢复节点签名文件](Mainnet-Validator-Keybackup.md)

### 4. 节点配置升级
1. 升级节点配置
``` 
./lambda upgrade
```
会自动升级`lambda.toml`的配置，同时创建`identity`目录

2. 更新节点`chain-id`
```
./lambdacli config chain-id lambda-chain-5.1
```

### 5. 配置种子节点  
`编辑~/.lambda/config/config.toml文件，将文件中的seeds字段的值替换如下`
```
72e1dd22f2c3effc4e6ff842035f109480a997ae@hk.mainnet.lambdastorage.com:26656

```

如果上面节点连接有问题，可以使用下面的任一种子节点

国内种子节点推荐
```
vim ~/.lambda/config/config.toml

节点列表
72e1dd22f2c3effc4e6ff842035f109480a997ae@hk.mainnet.lambdastorage.com:26656
d3440b0b7a0ccf419f506a1242431813cf8a699c@hhht.mainnet.lambdastorage.com:26656
98a0a749080b367d218f68b628b2db3d8d175af9@zjk.mainnet.lambdastorage.com:26656
7bfaaba8ffcc2cf20304f8992db915b2604ed720@bj.mainnet.lambdastorage.com:26656 
```

国外种子节点推荐
```
vim ~/.lambda/config/config.toml

节点列表
ea7d31b6fd17d06390445b5e2c2d40a3762c9ea3@tokyo1.mainnet.lambdastorage.com:26656 (推荐)
2274be959a4598a789791edf811546c20b68495f@tokyo2.mainnet.lambdastorage.com:26656
```

### 6. 配置lambda.toml
修改配置文件
```
vi ~/.lambda/config/lambda.toml
```
```

minimum-gas-prices = ""

[log]
level = "info"
output_file = "stdout"

# 服务需要监听的地址
# 以本机内网IP为 192.168.10.30，端口映射的外网IP为 200.200.200.300 为例
[server]
# 对外提供服务的地址，推荐配置为内网地址做端口映射到外网IP
address = "192.168.10.30:12000"
private_address = "127.0.0.1:12001"
debug_log_traffic = "false"

[kad]
# DHT接入节点地址，存储网络提供，可填写多个
bootstrap_addr = [
                  "zjk.mainnet.lambdastorage.com:12000",
                  "hhht.mainnet.lambdastorage.com:12000",
                  "bj.mainnet.lambdastorage.com:12000",
                  "hk.mainnet.lambdastorage.com:12000",
                  "tokyo1.mainnet.lambdastorage.com:12000",
                  "tokyo2.mainnet.lambdastorage.com:12000",]
bootstrap_backoff_max = "30s"
bootstrap_backoff_base = "1s"
db_path = "/root/.lambda/kademlia"
# 对外暴露的提供服务的地址
external_address = "200.200.200.300:12000"
alpha = 3

[kad.routing_table_config]
bucket_size = 20
replacement_cache_size = 5

[discov]
discovery_interval = "3m0s"

```

### 7. 覆盖genesis.json文件
```
\cp -rf ./genesis.json ~/.lambda/config/genesis.json
```

### 8. 启动节点  
```
./lambda start --p2p.laddr tcp://0.0.0.0:26656 --rpc.laddr tcp://0.0.0.0:26657 --daemonize --log.file /tmp/lambda.log
```

### 9. 启动rest-server服务
rest-server服务可提供给钱包、矿工和storagecli连接
```
nohup ./lambdacli rest-server --node tcp://0.0.0.0:26657 --laddr tcp://0.0.0.0:13659 >> /tmp/lambdacli.log 2>&1 &
```

### 10. 查看节点运行状态
#### 查看节点运行状态
```
./lambda status
```
返回结果如下即运行正常：
``` 
lambda.pid is running, pid is 5993
```

#### 停止节点 
如需要停止节点，可使用以下命令： 
```
./lambda stop
```
返回结果如下即停止成功：
``` 
stop daemon process from lambda.pid:5993 successfully
```

