# 主网Validator接入教程

**注意**  
节点接入前需要先同步当前服务器时间到最新时间
``` 
ntpdate -u ntp.api.bz
```
如服务器上无`ntpdate`命令，可使用`sudo yum install -y ntpdate`(CentOS)或`sudo apt-get install ntpdate -y`(Ubuntu)进行安装。

主网节点升级可参考：[主网Validator 0.6.2 升级教程](Mainnet-Validator-Upgrade-Guide.md)  

### 1. 下载安装包并解压
`创建目录并进入`
```
mkdir -p ~/LambdaIM && cd ~/LambdaIM
```
`下载安装包`
```
wget https://github.com/LambdaIM/launch/releases/download/v0.6.2/lambda-0.6.2-release.tar.gz

如下载缓慢可使用下面的链接：
wget http://download.lambdastorage.com/lambda/0.6.2/lambda-0.6.2-release.tar.gz
```

`解压安装包`
```
tar zxvf lambda-0.6.2-release.tar.gz && cd lambda-0.6.2-release
```

### 2. 初始化节点  
`将下面命令中的[your-moniker]替换成您自定义的节点名称，不用加中括号`  
`注意：这里的 your-moniker 必须使用英文，用于P2P网络`
```
./lambda init [your-moniker] --chain-id lambda-chain-5.1
```
如果初始化报错，可能是由于有老版本的测试网配置数据导致，可以通过下面的命令清除错误数据
```
rm ~/.lambda/config/config.toml ~/.lambda/config/genesis.json ~/.lambda/config/addrbook.json
```
```
./lambda unsafe-reset-all
```

**注意**

不要删除~/.lambda/config下的`priv_validator_key.json`和`node_key.json`文件，
如果丢失会导致节点无法再正常加入共识网络，请节点注意备份

[备份和恢复节点签名文件](Mainnet-Validator-Keybackup.md)

### 3. 覆盖genesis.json文件
```
\cp -rf ./genesis.json ~/.lambda/config/genesis.json
```

### 4. 配置节点
`要确保机器已开启端口26656, 26657`
```
./lambdacli config node tcp://0.0.0.0:26657
./lambdacli config chain-id lambda-chain-5.1
./lambdacli config trust-node true
```

### 5. 配置种子节点  
编辑`~/.lambda/config/config.toml`文件，将文件中的seeds字段的值替换如下
```
72e1dd22f2c3effc4e6ff842035f109480a997ae@hk.mainnet.lambdastorage.com:26656

```

如果上面节点连接有问题，可以使用下面的任一种子节点

国内种子节点推荐
```
72e1dd22f2c3effc4e6ff842035f109480a997ae@hk.mainnet.lambdastorage.com:26656
d3440b0b7a0ccf419f506a1242431813cf8a699c@hhht.mainnet.lambdastorage.com:26656
98a0a749080b367d218f68b628b2db3d8d175af9@zjk.mainnet.lambdastorage.com:26656
7bfaaba8ffcc2cf20304f8992db915b2604ed720@bj.mainnet.lambdastorage.com:26656 
```

国外种子节点推荐
```
2274be959a4598a789791edf811546c20b68495f@tokyo2.mainnet.lambdastorage.com:26656
```

**注意**

当前支持配置多个种子节点，通过`,`隔开  
切换节点后需要kill掉节点服务并且重启

### 6. 配置lambda.toml
需要修改配置文件`~/.lambda/config/lambda.toml`中的`kad.external_address`
```shell hl_lines="24 25"

minimum-gas-prices = ""

[log]
level = "info"
output_file = "stdout"

[server]
address = "0.0.0.0:12000"
private_address = "127.0.0.1:12001"
debug_log_traffic = "false"

[kad]
# DHT接入节点地址，存储网络提供，可填写多个
bootstrap_addr = [
                  "zjk.mainnet.lambdastorage.com:12000",
                  "hhht.mainnet.lambdastorage.com:12000",
                  "bj.mainnet.lambdastorage.com:12000",
                  "hk.mainnet.lambdastorage.com:12000",
                  "tokyo2.mainnet.lambdastorage.com:12000",]
bootstrap_backoff_max = "30s"
bootstrap_backoff_base = "1s"
db_path = "/root/.lambda/kademlia"
# 需要修改对外暴露的提供服务的地址，以外网IP为 200.200.200.300 为例
external_address = "200.200.200.300:12000"
alpha = 3

[kad.routing_table_config]
bucket_size = 20
replacement_cache_size = 5

[discov]
discovery_interval = "3m0s"

```

### 7. 启动节点  
#### 从零块高同步块（二选一）  
```
./lambda start --p2p.laddr tcp://0.0.0.0:26656 --rpc.laddr tcp://0.0.0.0:26657 --daemonize --log.file /tmp/lambda.log
```

#### 使用社区提供的区块链数据包启动节点（二选一）
从零块高同步块耗时较长，可使用社区提供的区块链数据包启动节点  

下载数据压缩包lambda_0.6.2_data.tar.gz
``` 
wget http://download.lambdastorage.com/lambda/0.6.2/lambda_0.6.2_data.tar.gz
```
解压`lambda_0.6.2_data.tar.gz`到`~/.lambda/data/`目录下（解压过程耗时较长，请耐心等待）
``` 
tar -zxvf lambda_0.6.2_data.tar.gz -C ~/.lambda/data/
```
启动节点
```
./lambda start --p2p.laddr tcp://0.0.0.0:26656 --rpc.laddr tcp://0.0.0.0:26657 --daemonize --log.file /tmp/lambda.log
```

### 8. 添加账户  
`将[your-account-name]替换成您自定义的账户名称，需要设置您的账户密码，不用加中括号`
```
./lambdacli keys add [your-account-name]
```

```如果是钱包创建的账户导入，则通过钱包创建账户时候的助记词进行操作```
```
./lambdacli keys add [your-account-name] --recover
```
输入命令后按照提示输入密码和助记词即可


### 9. 提交地址
提交上一步命令中返回的账户地址，用钱包签名并在质押系统内提交，我们会在收到后一定时间内转账

### 10. 创建 Validator  
创建Validator需要如下信息  
* pubkey -- 通过命令`./lambda tendermint show-validator` 获取  
* moniker -- 这里的`moniker`名称是您的`Validator`名称，可以使用中文(与第2步的moniker可以不同),  
             如果您已经创建，后面的FAQ中也有修改该名称的命令介绍  
* your-account-name -- 您在第7步中设置的账户名称  

`获取上述信息后，填充如下命令并执行（过程中会提示输入账号密码），即可创建Validator, 注意：所有参数不需要中括号`
```
./lambdacli tx staking create-validator \
  --amount 666666666utbb \
  --pubkey [your-cons-pubkey] \
  --moniker "[your-moniker]" \
  --from [your-account-name] --broadcast-mode block 
```

执行完上述命令后，会返回类似如下信息，destination-validator 即 Validtor 的操作地址
```
Response:
  Height: 617
  TxHash: 9B67980CFAE286B220B912549D4288119BEDAA7B74B831FA999C3AA60089B85C
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 121675
  Tags: 
    - action = create_validator
    - destination-validator = lambdavaloper1g2wgwnrdhj29v62jh9nj8kxml48dg3sfrujk2s
    - moniker = ohoh-11
    - identity =
```

Validator 的操作地址也可通过命令获取
```
./lambdacli keys show [your-account-name] --bech val
```


### 11. 启动rest-server服务
rest-server服务可提供给钱包、矿工和storagecli连接
```
nohup ./lambdacli rest-server --node tcp://0.0.0.0:26657 --laddr tcp://0.0.0.0:13659 >> /tmp/lambdacli.log 2>&1 &
```

### 12. 查看节点运行状态
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



[备份和恢复节点签名文件](Mainnet-Validator-Keybackup.md)

**注意**

当前已经成为validator的节点，在以下情况下会被惩罚，共识网络会扣除节点质押的utbb，并且把  
节点移出validator集合

1.对块进行双签，惩罚为  
- 扣除 1% 质押的TBB  
- 监禁三天  
（注意不要让节点出现双签情况！！！）  
双签场景：不同机器使用同一`priv_validator_key.json`文件启动节点  

2.在最近的10000个块中对少于500个块签名(掉线1天左右)，惩罚为  
- 扣除 0.01% 质押的TBB   
- jail 10分钟  

被移出的节点需要做如下操作重新加入共识网络

1. 如果不满足validator的最低质押要求`666,666,666utbb`, 需要发起质押补足扣除的utbb，可进入浏览器——验证节点——节点详情——质押列表——查看当前节点账户地址质押代币数量 即为当前已质押代币数量
命令示例参考  
```
./lambdacli tx staking delegate [validator-address] [amount-of-utbb] --from [your-account-name]
```

2. 发起`unjail`消息来重新加入共识网络
被`jail`之后的节点需要等待10分钟的惩罚来发起`unjail`命令

```
./lambdacli tx slashing unjail --from [your-account-name]
```

## FAQ
[主网接入帮助](FAQ.md)
