# 测试网0.4.8同步节点 接入教程

### 1. 下载安装包并解压
创建目录并进入
```
mkdir -p ~/LambdaIM && cd ~/LambdaIM
```
下载安装包
```
wget https://github.com/LambdaIM/launch/releases/download/v0.4.8/lambda-0.4.8-testnet.tar.gz

如下载缓慢可使用下面的链接：
wget http://download.lambdastorage.com/lambda/0.4.8/lambda-0.4.8-testnet.tar.gz
```

解压安装包
```
tar zxvf lambda-0.4.8-testnet.tar.gz && cd lambda-0.4.8-testnet
```

### 2. 初始化节点  
将下面命令中的[your-moniker]替换成您自定义的节点名称，不用加中括号`  
`注意：这里的 your-moniker 必须使用英文，用于P2P网络
```
./lambda init [your-moniker] --chain-id lambda-chain-test4.8
```
如果初始化报错，可能是由于有老版本的配置数据导致，可以通过下面的命令清除错误数据
```
rm -rf ~/.lambda/config/config.toml ~/.lambda/config/genesis.json ~/.lambda/identity
./lambda unsafe-reset-all
```

**注意**

不要删除~/.lambda/config下的`priv_validator_key.json`和`node_key.json`文件，
如果丢失会导致节点无法再正常加入共识网络，请节点注意备份

### 3. 覆盖genesis.json文件
```
\cp -rf ./genesis.json ~/.lambda/config/genesis.json
```

### 4. 配置种子节点  
修改`~/.lambda/config/config.toml`文件，将文件中的seeds字段的值替换如下
```
vim ~/.lambda/config/config.toml
seeds = "3da3b249f4f1afd0efdd6f4676972fdc7af0ea6b@47.94.129.97:26656"
```

测试网目前可选种子节点列表：
```
e02882af5bdafa5aec086c32b8398c268d2337f1@47.93.196.236:26656
3da3b249f4f1afd0efdd6f4676972fdc7af0ea6b@47.94.129.97:26656
559f3aeb13b58e611c95fdc6b34446de81cc470d@39.105.148.217:26656
9162e0c3494d8d32acd6c5bc48d1066f2cb362e6@182.92.66.63:26656
```

**注意**
当前支持配置多个种子节点，通过`,`隔开  
切换节点后需要kill掉节点服务并且重启

### 5. 配置lambda.toml
修改`~/.lambda/config/lambda.toml`文件
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
# DHT接入节点地址，存储网络提供，可填写多个，以 47.94.129.97:13000 为例
# 可选dht地址：39.105.148.217:13000/47.94.129.97:13000/47.93.196.236:13000/182.92.66.63:13000
bootstrap_addr = "47.94.129.97:13000"
bootstrap_backoff_max = "30s"
bootstrap_backoff_base = "1s"
db_path = "/root/.lambda/kademlia"
external_address = "200.200.200.300:12000"
alpha = 3

[kad.routing_table_config]
bucket_size = 20
replacement_cache_size = 5

[discov]
discovery_interval = "3m0s"
```

### 6. 下载和解压社区提供的区块链数据包
下载数据压缩包lambda_0.4.8_data.tar.gz
``` 
wget http://download.lambdastorage.com/lambda/0.4.8/lambda_0.4.8_data.tar.gz
```
解压`lambda_0.4.8_data.tar.gz`到`~/.lambda/`目录下（解压过程耗时较长，请耐心等待）
``` 
tar -zxvf lambda_0.4.8_data.tar.gz -C ~/.lambda/
```

### 7. 启动节点  
```
./lambda start --p2p.laddr tcp://0.0.0.0:26656 --rpc.laddr tcp://0.0.0.0:26657 --daemonize --log.file /tmp/lambda.log
```
说明：  
--daemonize以后台方式启动   
--log.file /tmp/lambda.log 日志输出/tmp/lambda.log文件里，可修改为其他目录，不添加参数则无日志输出

#### 停止节点
如需停掉节点，执行以下命令
```
./lambda stop

返回如下结果即为停止成功：
stop daemon process from lambda.pid:28638 successfully
```

#### 查看节点状态
``` 
./lambda status

返回结果如下，即节点正在运行：
lambda.pid is running, pid is 28800

返回结果如下，即节点未运行：
daemon have stoped
```


