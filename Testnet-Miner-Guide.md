# 矿工0.2.4接入教程

1个miner对应多个storagenode   

* [配置miner](#配置miner节点)
* * [1. 下载安装包并解压](#1下载安装包并解压)
* * [2. 配置lambdacli](#2配置lambdacli)
* * [3. 添加矿工账户](#3添加矿工账户)
* * [4. 创建miner](#4创建miner)
* * [5. 初始化storagenode](#5初始化storagenode)
* * [6. storagenode配置和启动](#6storagenode配置和启动)
* * [7. 矿工创建卖单](#6矿工创建卖单)
* * [8. 创建买单](#7创建买单)
* [文件上传和查看](#文件上传和查看)
* * [1. 配置](#1配置)
* * [2. 上传文件](#2上传文件)
* [挖矿](#挖矿)
---
* [提取订单收益](#提取订单收益)
* [测试网络连通](#测试网络连通)

矿工和存储节点0.2.4升级参考：[Storage0.2.4升级](Testnet-Storage-Upgrade.md)

## 配置矿工和存储节点

### 1下载安装包并解压

创建目录并进入 

```
mkdir -p ~/LambdaIM && cd ~/LambdaIM
```
下载安装包
```
wget https://github.com/LambdaIM/launch/releases/download/Storage0.2.4/lambda-storage-0.2.4-testnet.tar.gz

如下载缓慢可使用下面的链接：
wget http://download.lambdastorage.com/lambda-storage/0.2.4/lambda-storage-0.2.4-testnet.tar.gz
```
解压安装包
```
tar zxvf lambda-storage-0.2.4-testnet.tar.gz
```
进入解压后的目录
```
cd lambda-storage-0.2.4-testnet
```

### 2配置lambdacli

```
./lambdacli config node tcp://[nodeip]:26657
```
[nodeip] 为自己质押的验证节点公网IP

可选Lambda官方验证节点IP如下:
```
47.93.196.236
47.94.129.97
39.105.148.217
182.92.66.63
```

```
./lambdacli config chain-id lambda-chain-test4.5
```
```

./lambdacli config trust-node true
```
```
./lambdacli config dht-gateway-address [kad.external_address]
```
[kad.external_address] 为验证节点配置lambda.toml中的kad.external_address，可填写自己质押的验证节点dht地址

可选Lambda官方dht-gateway-address如下:
```
47.93.196.236:13000
47.94.129.97:13000
39.105.148.217:13000
182.92.66.63:13000
```
### 3添加矿工账户
将[your-account-name]替换成您自定义的矿工账户名称，需要设置您的账户密码，不用加中括号  
矿工子账户用来提交挖矿声明和挖矿证明，每笔交易需要一定的手续费，需要保证矿工子账户余额大于1000LAMB

提示：也可以使用钱包进行添加矿工账户、导入/导出矿工子账户、转账、质押等操作

以下两个步骤只需选一个执行
#### (二选一)新创建矿工账户及子账户
```
./lambdacli keys add [your-account-name] --generate-miner 
```

#### (二选一)已有矿工账户时，导入矿工和生成子账户

如果是钱包创建的账户导入，则通过钱包创建账户时候的助记词进行导入

```
./lambdacli keys add [your-account-name] --recover 
```
输入命令后按照提示输入密码和助记词即导入账户成功

然后生成矿工子账户：
```
./lambdacli keys create-miner [your-account-name] 
```
输入命令后按照提示输入助记词即可


### 4创建miner

#### 质押资产到节点
```
./lambdacli tx staking delegate [validator-address] [amount-of-utbb] \
--from [your-account-name] --broadcast-mode block -y
```
- [validator-address] 质押的节点地址，可指定 自己的验证节点地址 或 Lambda官方节点地址，节点地址可通过浏览器查找 [http://testbrowser.lambda.im/#/](http://testbrowser.lambda.im/#/) 或询问节点  
- [amount-of-utbb] 为质押到节点的utbb数量，不得少于1TBB（1TBB=1000000utbb）  
- [your-account-name] 是您在第3步创建的账户名称  

```
例如质押20TBB到节点lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl：
./lambdacli tx staking delegate lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl 20000000utbb \
--from myaccount --broadcast-mode block -y
```

可选Lambda官方节点地址：
```
lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl
lambdavaloper1thj5fv8d0dsh3aealhpxm9mvgxjfh87suwuj2h
lambdavaloper1a83p8s9gs5hua09xn5ktmahepst3vzg9u2l20d
lambdavaloper1r340rrv9fs95gqy5087e2mtz82vvwrglt6amx3
```
 


#### 初始化矿工及配置
1. 初始化矿工
```
./minernode init
```
会生成矿工配置文件~/.lambda_miner/config/config.toml

2. 修改配置文件
参考如下说明手动修改配置文件  
`vi ~/.lambda_miner/config/config.toml`
```

[build]
version = "0.2.4"
commit = "030c696bc6829cfafb3d240d66058b16b41aa460"
mode = "release"

# 服务需要监听的地址
# 以本机内网IP为 192.168.10.10，端口映射的外网IP为 200.200.200.100 为例
[server]
# 对外提供服务的地址，推荐配置为内网地址做端口映射到外网IP
address = "192.168.10.10:13000"
# 对内提供服务的地址，主要是给StorageNode使用，推荐配置为内网地址
private_address = "192.168.10.10:13001"

[kad]
# DHT接入节点地址，存储网络提供，可填写多个，以 47.94.129.97:13000 为例
# 可填写自己质押的验证节点配置lambda.toml中的 kad.external_address
# 可选官方dht地址：39.105.148.217:13000/47.94.129.97:13000/47.93.196.236:13000/182.92.66.63:13000
bootstrap_addr = ["47.94.129.97:13000"]
# this should listen at Public IP
## 对外暴露的提供服务的地址
external_address = "200.200.200.100:13000"

[log]
level = "info"
output_file = "stdout"

[miner]
# ensure_level=0会多占用磁盘1/6空间，ensure_level=1会多占用1/3空间
ensure_level = "0"
#root access key，不能为空
root_secret_seed = "aaa"

[db]
# db config
lru_cache = "0"
keep_log_file_num = "16"
write_buffer_size = "268435456"
recycle_log_file_num = "0"
target_file_size_base = "268435456"
max_write_buffer_number = "25"
max_bytes_for_level_base = "4294967296"
level_0_stop_writes_trigger = "24"
target_file_size_multiplier = "1"
max_background_compactions = "2"
max_bytes_for_level_multiplier = "2"
level_0_slowdown_writes_trigger = "17"
level_0_file_num_compaction_trigger = "8"
level_compaction_dynamic_level_bytes = "0"
compaction_algorithm = "0"
rate_bytes_per_sec = "67108864"
data_backup_path = ""
```

#### 查看矿工子账户地址
将第三步生成的[your-account-name]_miner_key.json文件重命名为`default_miner_key.json`并移动到`~/.lambda_miner/config/`:
```
mv [your-account-name]_miner_key.json ~/.lambda_miner/config/default_miner_key.json
```

查询矿工子账户地址：
```
./minernode show-address 
返回如下结果：
Miner Address: lambda1lhhgvyaepf92mtx5zj49fseexr3g3njlz4jmgt (lambdamineroper1lhhgvyaepf92mtx5zj49fseexr3g3njlk67uak) //矿工账户地址
Mining Address: lambda10m4xmmvwat9a53rf47pjjpn3tecdk64urd5qt9 //矿工子账户地址
```

#### 给子账户转账
[miningAddr] 为上面查询到的矿工子账户地址（1LAMB=1000000ulamb）
```
./lambdacli tx send [miningAddr] 1000000000ulamb --from [your-account-name] --broadcast-mode block -y
```

#### 创建矿工
[miner-name] 是您在第3步创建的矿工账户名称。  
[miningAddr] 为矿工子账户地址。
[dht-id] 使用`./minernode info`查询
```
./minernode info
返回结果：
               version: 0.2.4
                dht id: G4xW3UHMfFnTmaRMZUJ7PKcfvr9YTTFyekcsRxKDZZD9  //创建矿工时会用到此dht-id
server.private_address: 172.17.159.130:15001
        server.address: 0.0.0.0:26654
  kad.external_address: 39.106.153.62:26654
    kad.bootstrap_addr: [39.106.153.62:26650 172.17.159.130:26652]
      Ensure-level = 0: 1/6 of disk-space would be used for data-replicating

创建矿工命令：
./lambdacli tx market create-miner --dht-id [dht-id] --mining-address [miningAddr] --from [miner-name] --broadcast-mode block -y
```
#### 启动矿工服务
[log_file_path] 指定矿工日志完整路径
```
./minernode run --query-interval 5 --daemonize --log.file [log_file_path]

如[your-account-name]_miner_key.json没有移动到~/.lambda_miner/config/default_miner_key.json，则加上--key-file参数启动：
./minernode run --query-interval 5 --daemonize --log.file [log_file_path] --key-file [filepath/your-account-name]_miner_key.json

```


#### 查看矿工服务进程
```
./minernode run --status
```
```
返回结果如下即进程在运行中：
minernode.pid is running, pid is 19276
```

#### 停止矿工服务
```
./minernode run --stop
```
```
返回结果如下即停止矿工服务成功：
stop daemon process from minernode.pid:19276 successfully
```

### 5初始化storagenode

```
./storagenode init
```
生成存储节点配置文件~/.lambda_storage/config/config.toml，参考如下第6步进行配置

### 6storagenode配置和启动
[storagenode配置启动参考](./Testnet-Storagenode-Configure.md)

### 7矿工创建卖单

加上--normal参数（赔付比率rate为0.5）的是普通卖单，价格只能等于5000000ulamb（1LAMB=1000000ulamb）；
不加--normal参数（赔付比率等于1）的为优质卖单，优质卖单可指定大于等于5000000ulamb的任意价格。  
设置需要卖出的空间大小size；   
最小购买空间min-size不能小于1GB;  
最小购买时长min-buy-duration不能小于1month;  
最大购买时长max-buy-duration不能大于60month。

注意：测试网中尽量挂优质卖单（不加--normal参数），这样创建买单时才能指定卖单ID匹配到自己矿工的卖单。

#### 创建普通卖单

一个矿工可创建多笔卖单，卖单总空间不能大于质押TBB数量，例如：一个矿工质押了1000000utbb（即1TBB），创建卖单总空间不能超过1TB（即1000GB）

```
./lambdacli tx market create-sellorder --price 5000000ulamb  \
--normal \
--size [size]GB \
--market-name LambdaMarket \
--min-size [min-size]GB \
--min-buy-duration [min-buy-duration]month \
--max-buy-duration [max-buy-duration]month \
--from [miner-name] --broadcast-mode block -y
```

#### 创建优质卖单

```
./lambdacli tx market create-sellorder --price [sellorder-price]  \
--size [size]GB \
--market-name LambdaMarket \
--min-size [min-size]GB \
--min-buy-duration [min-buy-duration]month \
--max-buy-duration [max-buy-duration]month \
--from [miner-name] --broadcast-mode block -y
```
#### 查询卖单
```
查询账户地址：
./lambdacli keys show [miner-name] --address
根据账户地址查看矿工卖单：
./lambdacli query market miner-sellorders [address] [page] [limit] 

例如：
查看账户名为miner2的地址：./lambdacli keys show miner2 --address
返回结果：lambda1k6rxrmly7hz0ewh7gth2dj48mv3xs9yz8ffauw

./lambdacli query market miner-sellorders lambda1k6rxrmly7hz0ewh7gth2dj48mv3xs9yz8ffauw 1 10
返回结果：
SellOrder
  OrderId:            54F82FBD979BE150C8B3246D82DDF60F043129EE  //卖单ID，取消卖单或创建优质买单时需要用到此ID
  Address:            lambdamineroper1k6rxrmly7hz0ewh7gth2dj48mv3xs9yznx96fn
  Price:              5000000
  Rate:               1.000000000000000000  //rate等于1，则该卖单为优质卖单
  Amount:
  SellSize:           400
  UnUseSize:          0
  Status:             1
  CreateTime:         2019-11-04 12:02:24.379880755 +0000 UTC
  CancelTimeDuration: 1h0m0s
  MarketAddress:      lambdamarketoper1thj5fv8d0dsh3aealhpxm9mvgxjfh87srk3887
  MachineName:        machine1
  MinBuySize:         1
  MinDuration:        720h0m0s
  MaxDuration:        43200h0m0s
```

#### 取消卖单

根据SellOrderID取消卖单
```
./lambdacli tx market cancel-order [orderId] --from [miner-name] --broadcast-mode block -y
```


### 8创建买单
矿工不能买自己的卖单，只能换其他账户来挂买单。

创建优质买单需要指定对应优质卖单SellOrderID。

account-name为当前账户的名称；
duration为购买时长；
size为需要购买的空间，不小于对应卖单指定的最小购买空间。

#### 创建普通买单

```
 ./lambdacli tx market create-buyorder --from [account-name] \
 --duration [buy-duration]month --market-name LambdaMarket \
 --size [size]GB --broadcast-mode block -y
```

#### 创建优质买单
[orderId] 可指定1个或多个优质卖单ID，指定多个卖单ID时以逗号分隔，例如：58941CFFEEA859AED51172F0F9DF3E77293D2E12,54F82FBD979BE150C8B3246D82DDF60F043129EE
```
./lambdacli tx market create-buyorder --sellorder-id [orderId] \
--from [your-account-name] --duration [buy-duration]month \
--market-name LambdaMarket --size [size]GB --broadcast-mode block -y
```

#### 查询匹配订单

```
查询账户地址：
./lambdacli keys show [account-name] --address
根据账户地址查看匹配订单：
./lambdacli query market matchorders [address] [page] [limit]

例如：
./lambdacli keys show buyaccount --address
返回结果：lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr
./lambdacli query market matchorders lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr 1 10
返回结果：
MatchOrder
  OrderId:               05F09566BA4397BC9EB378EC202676D3FFCAF660   //匹配订单ID，上传文件时需要用到该ID
  AskAddress:            lambdamineroper1k6rxrmly7hz0ewh7gth2dj48mv3xs9yznx96fn
  BuyAddress:            lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr
  SellOrderId:           58941CFFEEA859AED51172F0F9DF3E77293D2E12
  BuyOrderId:            F3B5BDE351253E1D47DA7CEB24C0E4BAB5BDA808
  Price:                 5000000
  Size:                  20
  CreateTime:            2019-11-01 13:20:58.296399278 +0000 UTC
  EndTime:               2019-12-01 13:20:58.296399278 +0000 UTC
  CancelTimeDuration:    1h0m0s
  WithDrawTime:          2019-11-01 13:20:58.296399278 +0000 UTC
  Status:                0
  MarketAddress:         lambdamarketoper1thj5fv8d0dsh3aealhpxm9mvgxjfh87srk3887
  MachineName:           machine1
  UserPay:               100000000ulamb
  MinerPay:              100000000ulamb
  PubKey:                PubKeyEd25519{5AD2B4ECA8C33922A8228A5217900E5725BF3013639118D1002B6A413971F9DC}
  PeerId:                bdd4da2a3021d30e8f215dba64716cec02cdb8a7
  DhtId:                 5i6fXKQJoktPVmt9PAfZ18RN7DG6tghQN7SK7A3Bq4Rc
```


## 文件上传和查看

### 1配置

初始化storagecli
```
./storagecli init
```
初始化storagecli 后会默认生成配置文件~/.lambda_storagecli/config/user.toml

如已备份旧版storagecli配置文件，可使用旧文件覆盖新的
```
\cp -rf ~/lambda_bak/user.toml ~/.lambda_storagecli/config/user.toml
```

如未部署过storagecli，需参考如下说明手动修改配置文件  
`vi ~/.lambda_storagecli/config/user.toml`

```
[broker]
# dht_gateway_addr为验证节点的dht服务 IP和端口；
# 可以是自己质押的验证节点配置的kad.external_address，这里以 47.94.129.97:13000 为例
# 可选官方dht地址：39.105.148.217:13000/47.94.129.97:13000/47.93.196.236:13000/182.92.66.63:13000
dht_gateway_addr = "39.105.148.217:13000" 
# validator_addr为验证节点IP和端口，可以是自己质押的验证节点rest-server服务指定的laddr地址
# 可选官方地址：39.105.148.217:13659/47.94.129.97:13659/47.93.196.236:13659
validator_addr = "39.105.148.217:13659"   

[gateway]
# local listen address
address = "0.0.0.0:9002"
# for login web UI
access_key = "accesskey"
secret_key = "secretkey"
```
同步所有订单的token

account-name 为发起买单账户名称
```
./storagecli token sync [account-name]
```


### 2上传文件

文本/图片/视频/音频/可执行文件/压缩包文件可正常上传。上传源文件路径为绝对路径。

- orderId为匹配单orderID;
- account-name为发起买单账户名称；
- bucket-name 可设置为长度不小于3且不大于64位的英文大小写，一个订单下可以有多个bucket

#### 上传文件

```
创建bucket：
LAMBDA_ORDER_ID=[orderId] ./storagecli mb [account-name] lamb://[bucket-name]/

上传文件：
LAMBDA_ORDER_ID=[orderId] ./storagecli cp [account-name] [srcPath] lamb://[bucket-name]/ 

```


#### 查看上传文件列表

```
LAMBDA_ORDER_ID=[orderId] ./storagecli ls lamb://[bucket-name]/ 
```

### 3查看订单和矿工状态
```
./storagecli order list [account-name]
```

例如
``` 
./storagecli order list myaccount 

OrderId                                  |Expire           |Used/Total      |ProviderStatus
81B7663F9D5F40A37F4875FC1B95E2C5E1CD7FEA |2020-04-24 09:00 |100 GiB/100 GiB |Maintaining
EF667304E33C6AAB9D56F04DF878FD93A5153B6D |2020-04-24 09:00 |100 GiB/100 GiB |Invalid
Total: 2
```
ProviderStatus为矿工状态，Avaialable为正常状态，Maintaining矿工正在维护，Invalid 矿工失效

## 挖矿
#### 矿工挖矿

矿工每接受文件`8GB`文件会对应生成一个声明，所有声明有效期为1个月，每个出块周期（大约每6s出一个块）会由共识网络发起挑战，挑战声明成功并提交挖矿证明的矿工就会得到一笔收益。


1. 有有效声明的矿工有挖矿权利；
2. 矿工已存文件每满8G可生成1个声明；
3. 单个矿工声明越多，该矿工被挑选到的概率越大。


#### 挖矿收益
矿工收益 = 单个区块增发量 * （43% * 95% / 挖矿的矿工数量） + 单个区块增发量 * （43% * 5% / 挖矿的矿工数量 ）* 矿工质押量在节点质押量的占比 * 75%

```
比如单个区块增发量为100LAMB，全网共1个节点该节点质押666TBB，全网共10个矿工分别质押1TBB且分别有10个声明。
则单个矿工单个区块得到的挖矿奖励为4.085LAMB= 100LAMB * 43% * 95% / 10 + 100LAMB * 43% * 5% / 10 * 1/676 * 75%
```

## 提取订单收益
[提取单个匹配订单收益](./docs/lambdacli/tx/market/withdraw-miner.md)  
[批量提取匹配订单收益](./docs/lambdacli/tx/market/miner-withdraw-count.md)

## 测试网络连通

当启动miner、storagenode、或上传文件时有报错，请使用以下命令进行排查。

### 1测试miner服务

```
./minernode info --test
返回结果均为successful即正常：
               version: 0.2.4
                dht id: G4xW3UHMfFnTmaRMZUJ7PKcfvr9YTTFyekcsRxKDZZD9
server.private_address: 172.17.159.130:15001   successful
        server.address: 0.0.0.0:26654    successful
  kad.external_address: 39.106.153.62:26654    successful
    kad.bootstrap_addr: [39.106.153.62:26650 172.17.159.130:26652]    successful successful
      Ensure-level = 0: 1/6 of disk-space would be used for data-replicating
```
### 2测试storagenode服务

```
./storagenode info network --test

返回结果均为successful即正常：
               version: 0.2.4
                dht id: 3mta4YEgHB43RHYE83aWBouvFNNCtSc832siEwmcTUsZ
  storage.storage_name: sn1
 storage.miner_address: 172.17.159.130:15001   successful
server.private_address: 172.17.159.130:16001   successful
        server.address: 0.0.0.0:26660    successful
  kad.external_address: 39.106.153.62:26660    successful
    kad.bootstrap_addr: [172.17.159.130:26650 172.17.159.130:26652]     successful successful

```

### 查看存储节点磁盘空间
```
./storagenode info disk
               version:  0.2.4
  storage.storage_name:  sn1
      storage.data_dir:  [/lambda/data/xvdd/store /lambda/data/xvde/store /lambda/data/xvdc/中文test/store /lambda/.1lambda_storage/store]

Disk                           |Total  |Used    |Free    |Order                                    |Reserved |Occupied
/lambda/data/xvdd/store        |18 GiB |8.9 GiB |8.8 GiB |753E54547CC66DB840E6C717C98492640B6E5CF8 |3.0 GiB  |540 MiB
                               |       |        |        |E15F0CCA09A8F92E401E322638CA777BC9EA24B8 |3.0 GiB  |1.9 GiB
/lambda/data/xvde/store        |18 GiB |592 MiB |17 GiB  |D3280F0343112CC35B864CFFEE96DE3D2F39F3C7 |12 GiB   |579 MiB
/lambda/data/xvdc/中文test/store |18 GiB |13 GiB  |4.6 GiB |DBE8C6D465D1701E71A7CBDF35E9F602A9CE55AE |6.0 GiB  |3.8 GiB

Reserved为订单预留的磁盘空间，Occupied为当前订单实际占用磁盘空间
```

## 备份和恢复存储文件
以防配置文件丢失，请提前做好文件备份：[存储网络文件备份](StorageFile-Backup.md)


