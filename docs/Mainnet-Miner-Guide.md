# 矿工0.2.7.1接入教程

1个miner下可注册多个storagenode   

0.2.7_rc3或0.2.7 升级0.2.7.1可参考：[storage0.2.7.1升级](Mainnet-Store-Upgrade.md)  

## 一、配置矿工和存储节点

### 1. 下载安装包并解压

!!! example ""
    1. 创建并进入目录 
    ```
    mkdir -p ~/LambdaIM && cd ~/LambdaIM
    ```
    2. 下载安装包
    ```
    wget https://github.com/LambdaIM/launch/releases/download/Storage0.2.7.1/lambda-storage-0.2.7.1.tar.gz
    ```
    如下载缓慢可使用下面的链接：
    ```
    wget http://download.lambdastorage.com/lambda-storage/0.2.7.1/lambda-storage-0.2.7.1.tar.gz
    ```
    3. 解压安装包
    ```
    tar zxvf lambda-storage-0.2.7.1.tar.gz
    ```
    4. 进入解压后的目录
    ```
    cd lambda-storage-0.2.7.1
    ```

### 2. 配置lambdacli

!!! example ""
    !!! abstract ""
        
        设置或切换链接的验证节点
        ```
        ./lambdacli config node tcp://[nodeip]:26657
        ```  
        
        - `[nodeip]` 为自己质押的验证节点`公网IP`
         
        [Lambda端口说明](Lambda-Node-Port.md)
              
    !!! abstract ""
        ```
        ./lambdacli config chain-id lambda-chain-5.1
        ./lambdacli config trust-node true
        ```
    
    !!! abstract ""
        ```
        ./lambdacli config dht-gateway-address [kad.external_address]
        ```   
               
        - `[kad.external_address]` 为验证节点配置`lambda.toml`中的`kad.external_address`，可填写自己质押的验证节点`dht`地址 
        
        可选Lambda官方`dht-gateway-address`如下:
        
        === "dht1"
            ```shell
            ./lambdacli config dht-gateway-address zjk.mainnet.lambdastorage.com:12000
            ```
        === "dht2"
            ```shell
            ./lambdacli config dht-gateway-address hhht.mainnet.lambdastorage.com:12000
            ```
        === "dht3"
            ```shell
            ./lambdacli config dht-gateway-address bj.mainnet.lambdastorage.com:12000
            ```
        === "dht4"
            ```shell
            ./lambdacli config dht-gateway-address hk.mainnet.lambdastorage.com:12000
            ```  
        === "dht5(国外)"
            ```shell
            ./lambdacli config dht-gateway-address tokyo1.mainnet.lambdastorage.com:12000
            ```
        === "dht6(国外)"
            ```shell
            ./lambdacli config dht-gateway-address tokyo2.mainnet.lambdastorage.com:12000
            ```              

### 3. 添加矿工账户

!!! example ""

    !!! abstract ""
        以下`新建矿工账户及子账户（新用户）`和`导入矿工账户及子账户（老用户）`只需选一个执行  
        
        === "新建矿工账户及子账户（新用户）"
            ```shell
            ./lambdacli keys add [your-account-name] \
            --generate-miner 
            ```
        === "导入矿工账户及子账户（老用户）"
            如果是钱包创建的账户导入，则通过钱包创建账户时候的助记词进行导入
            ```shell
            ./lambdacli keys add [your-account-name] \
            --generate-miner --recover 
            ```
            输入命令后按照提示输入密码和助记词后，即导入账户和生成矿工子账户成功
        
        - 将`[your-account-name]`替换成您自定义的矿工账户名称，需要设置您的账户密码，不用加中括号 
    
    !!! note  
        矿工子账户用来提交挖矿声明和挖矿证明，每笔交易需要一定的手续费，需要保证矿工子账户余额大于1000LAMB
    
    !!! tip
        也可以使用钱包进行添加矿工账户、导入/导出矿工子账户、转账、质押等操作

### 4. 创建和启动矿工

#### 4.1 质押资产到节点

!!! example ""
    ```
    ./lambdacli tx staking delegate [validator-address] [amount-of-utbb] \
    --from [your-account-name] --broadcast-mode block -y
    ```
    
    - `[validator-address]` 质押的节点操作地址（前缀lambdavaloper），可指定 `自己的验证节点操作地址` 或 `Lambda社区节点操作地址`，节点操作地址可通过浏览器查找 [http://explorer.lambda.im/#/](http://explorer.lambda.im/#/) 或询问节点  
    - `[amount-of-utbb]` 为质押到节点的 utbb 数量，不得少于 `1TBB`（`1TBB=1000000utbb`）  
    - `[your-account-name]` 是您在第 3 步创建的账户名称  
    
    可选Lambda官方节点操作地址(cv-moniker-1 / 2 / 3 / 4)：
    
    === "addr1"
        ```
        lambdavaloper1eypzf5cguwsgummfe02qklyyry9ujrw6n4n5rk
        ```
    === "addr2"
        ```
        lambdavaloper1vulk9gxlhfxq85axwcxtf77qpxstf6ygj0r0ek
        ```
    === "addr3"
        ```
        lambdavaloper1azylnnrlcvnkt3v0537rullcs8pruvjdf09v92
        ```
    === "addr4"
        ```
        lambdavaloper1mefs79zjd0g9k3v62zfwm47yffyuzdkvt9jwr4
        ```
        
    ??? note "展开查看质押示例"
         例如质押20TBB到节点 `lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl`
        ```
        ./lambdacli tx staking delegate lambdavaloper1vulk9gxlhfxq85axwcxtf77qpxstf6ygj0r0ek 20000000utbb --from myaccount --broadcast-mode block -y
        ``` 

#### 4.2 初始化矿工及配置

!!! example ""
    1. 初始化矿工
    ```
    ./minernode init 
    ```
    会生成矿工配置文件`~/.lambda_miner/config/config.toml`  
    2. 修改矿工配置
    
    !!! abstract ""
        
        === "修改矿工配置"
        
            以矿工所在机器的外网IP为 200.200.200.100 为例：
            ```       
            ./minernode config kad.external_address 200.200.200.100:13000
            
            ```
            
            ??? note "展开查看配置说明"
                ```shell hl_lines="26"              
                [build]
                version = "0.2.7.1"
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
                # DHT接入节点地址，存储网络提供，可填写多个
                # 可填写自己质押的验证节点配置lambda.toml中的 kad.external_address
                bootstrap_addr = [
                  "zjk.mainnet.lambdastorage.com:12000",
                  "hhht.mainnet.lambdastorage.com:12000",
                  "bj.mainnet.lambdastorage.com:12000",
                  "hk.mainnet.lambdastorage.com:12000",
                  "tokyo1.mainnet.lambdastorage.com:12000",
                  "tokyo2.mainnet.lambdastorage.com:12000",]
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

#### 4.3 查看矿工子账户地址

!!! example ""
    将第三步生成的`[your-account-name]_miner_key.json`文件重命名为`default_miner_key.json`并移动到`~/.lambda_miner/config/`:
    ```
    mv [your-account-name]_miner_key.json ~/.lambda_miner/config/default_miner_key.json
    ```
    
    查询矿工子账户地址：
    ```
    ./minernode show-address 
    ```
    
    !!! success "返回如下结果"
        ```shell hl_lines="2 3"
        Miner Address: lambda1lhhgvyaepf92mtx5zj49fseexr3g3njlz4jmgt 
        (lambdamineroper1lhhgvyaepf92mtx5zj49fseexr3g3njlk67uak)#矿工账户地址 和 矿工操作地址lambdamineroper
        Mining Address: lambda10m4xmmvwat9a53rf47pjjpn3tecdk64urd5qt9# 矿工子账户地址 
        ```


#### 4.4 给子账户转账

!!! example ""
    ```
    ./lambdacli tx send [miningAddr] 1000000000ulamb --from [your-account-name] --broadcast-mode block -y
    ```
    
    - `[miningAddr]` 为上面查询到的矿工子账户地址（`1LAMB=1000000ulamb`）
    - `[your-account-name]` 为你的账户名，需要保证该账户余额足够才能转账成功


#### 4.5 创建矿工

!!! example "" 
    查询当前矿工服务器的`dht id`:
    ```
    ./minernode info
    ```
    
    !!! success "返回如下结果"
        ```text hl_lines="2"
                       version: 0.2.7.1
                        dht id: G4xW3UHMfFnTmaRMZUJ7PKcfvr9YTTFyekcsRxKDZZD9 #创建矿工时会用到此dht-id
        server.private_address: 172.11.159.11:15001
                server.address: 0.0.0.0:26654
          kad.external_address: 39.106.153.11:26654
            kad.bootstrap_addr: [39.106.153.11:26650 172.11.159.11:26652]
              Ensure-level = 0: 1/6 of disk-space would be used for data-replicating
        ```
        
!!! example ""    
    创建矿工命令：
    ```
    ./lambdacli tx market create-miner --dht-id [dht-id] --mining-address [miningAddr] --from [miner-name] --broadcast-mode block -y
    ```
    
    * `[miner-name]` 是您在第3步创建的矿工账户名称。                 
    * `[miningAddr]` 为矿工子账户地址。                        
    * `[dht-id]` 使用`./minernode info`查询返回结果中的`dht id` 
    
    ??? note "展开查看创建矿工示例"
        ```
        ./lambdacli tx market create-miner --dht-id 75XGrP5ZtCcXm5EQfX1yzrVfyhRf7E3VKpB4iWiZGgNB --mining-address lambda1m6424w2rkkhd4jf3upgd8mgxu9vydc4mcng7y5 --from miner2 --broadcast-mode block -y
        ``` 
    
#### 4.6 启动矿工服务

!!! example ""
    启动矿工服务
    ```
    ./minernode run --query-interval 5 --daemonize --log.file [log_file_path]
    ```
    
    - `[log_file_path]` 指定矿工日志完整路径
    
    如`[your-account-name]_miner_key.json`没有移动到`~/.lambda_miner/config/default_miner_key.json`，则加上`--key-file`参数启动：
    ```
    ./minernode run --query-interval 5 --daemonize --log.file [log_file_path] --key-file [filepath/your-account-name]_miner_key.json
    ```

!!! example ""
    查看矿工服务进程
    ```
    ./minernode run --status
    ```
    
    !!! success "返回如下结果"
        ```
        minernode.pid is running, pid is 19276
        ```

??? note "展开查看停止矿工服务命令"
    停止矿工服务
    ```
    ./minernode run --stop
    ```
    
    !!! success "返回如下结果"
        ```
        stop daemon process from minernode.pid:19276 successfully
        ```

### 5. 初始化storagenode

!!! example ""
    ```
    ./storagenode init 
    ```
    生成存储节点配置文件`~/.lambda_storage/config/config.toml`，参考如下第6步进行配置

### 6. storagenode配置和启动
[storagenode配置启动参考](./Mainnet-Storagenode-Configure.md)

## 二、买卖单创建
### 1. 创建卖单

* 只能有赔付比率`rate`为 1的卖单，可设置大于等于指定市场的最低价格（lambdamarket市场最低价格为`5000000ulamb`）；
* 设置需要卖出的空间大小`size`；   
* 最小购买空间`min-size`不能小于1GB;  
* 最小购买时长`min-buy-duration`不能小于`1month`;  
* 最大购买时长`max-buy-duration`不能大于`60month`。

市场操作手册参考：[市场操作手册](./Market-Delegate-Operation-Guide.md)

#### 1.1 创建卖单

!!! example ""
    一个矿工可创建多笔卖单，卖单总空间不能大于质押TBB数量，例如：一个矿工质押了`1000000utbb`（即`1TBB`），创建卖单总空间不能超过`1TB`（即`1000GB`）

    ```
    ./lambdacli tx market create-sellorder --price [sellorder-price]  \
    --size [size]GB \
    --market-name lambdamarket \
    --min-size [min-size]GB \
    --min-buy-duration [min-buy-duration]month \
    --max-buy-duration [max-buy-duration]month \
    --from [miner-name] --broadcast-mode block -y
    ```
    
#### 1.2 查询卖单

!!! example ""
    查询账户地址：
    ```
    ./lambdacli keys show [miner-name] --address
    ```
    根据账户地址查看矿工卖单：
    ```
    ./lambdacli query market miner-sellorders [address] [page] [limit] 
    ```
    
    !!! 示例
        查看账户名为miner2的地址：
        ```
        ./lambdacli keys show miner2 --address
        ```
        返回结果：`lambda1k6rxrmly7hz0ewh7gth2dj48mv3xs9yz8ffauw`
        ```
        ./lambdacli query market miner-sellorders lambda1k6rxrmly7hz0ewh7gth2dj48mv3xs9yz8ffauw 1 10
        ```
        返回结果：
        ```shell hl_lines="2"
        SellOrder
          OrderId:            54F82FBD979BE150C8B3246D82DDF60F043129EE #卖单ID，取消卖单或创建买单时需要用到此ID
          Address:            lambdamineroper1k6rxrmly7hz0ewh7gth2dj48mv3xs9yznx96fn
          Price:              5000000
          Rate:               1.000000000000000000 
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

#### 1.3 取消卖单

!!! example ""
    根据SellOrderID取消卖单
    ```
    ./lambdacli tx market cancel-order [orderId] --from [miner-name] --broadcast-mode block -y
    ```


### 2. 创建买单

- `[account-name]` 为当前账户的名称；
- `[duration]` 为购买时长；
- `[market-name]` 为市场名称，lambda社区市场为`lambdamarket`，也可指定其他用户创建的market
- `[size]` 为需要购买的空间，不小于对应卖单指定的最小购买空间。
- `[orderId]` 必须要指定该参数，可指定1个或多个卖单ID，指定多个卖单ID时以逗号分隔，例如：`58941CFFEEA859AED51172F0F9DF3E77293D2E12,54F82FBD979BE150C8B3246D82DDF60F043129EE`

#### 2.1 创建买单

!!! example ""
    
    ```
    ./lambdacli tx market create-buyorder --sellorder-id [orderId] \
    --from [your-account-name] --duration [buy-duration]month \
    --market-name lambdamarket --size [size]GB --broadcast-mode block -y
    ```

#### 2.2 查询匹配订单  

!!! example ""  
    查询账户地址：
    ```
    ./lambdacli keys show [account-name] --address
    ```
    根据账户地址查看匹配订单：
    ```
    ./lambdacli query market matchorders [address] [page] [limit]
    ```
        
    !!! 示例    
        ```
        ./lambdacli keys show buyaccount --address
        ```
        返回结果：`lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr`
        ```
        ./lambdacli query market matchorders lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr 1 10
        ```
        返回结果：
        ```shell hl_lines="2 9 10"
        MatchOrder
          OrderId:               05F09566BA4397BC9EB378EC202676D3FFCAF660  #匹配订单ID，上传文件时需要用到该ID
          AskAddress:            lambdamineroper1k6rxrmly7hz0ewh7gth2dj48mv3xs9yznx96fn
          BuyAddress:            lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr
          SellOrderId:           58941CFFEEA859AED51172F0F9DF3E77293D2E12
          BuyOrderId:            F3B5BDE351253E1D47DA7CEB24C0E4BAB5BDA808
          Price:                 5000000
          Size:                  20
          CreateTime:            2019-11-01 13:20:58.296399278 +0000 UTC#匹配订单开始时间
          EndTime:               2019-12-01 13:20:58.296399278 +0000 UTC#匹配订单结束时间
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
  
  
### 3. 匹配订单续期 
1. 匹配订单未到期的，购买了空间的账户可使用`lambdacli tx market order-renewal`命令续期。  
2. 匹配订单已过期的，不能再进行续期；  
3. 同一匹配订单可多次续期；   
4. 续期后的匹配订单总时长（即结束时间减开始时间），不能超过60个月（1个月=30天)；  
5. 订单续期后，需要执行`minernode order refresh`使矿工获取匹配订单最新结束日期；  
6. 订单续期后，需要重新执行`storagecli token sync [account]`使存储获取订单最新日期   

续期成功后，可进入浏览器[http://explorer.lambda.im/#/](http://explorer.lambda.im/#/)搜索匹配订单ID，查看`匹配订单详情页`中结束时间是否延期了对应时长。  
或使用上面查询匹配订单命令`lambdacli query market matchorders`查看返回结果中的匹配订单结束时间（即`EndTime`）是否延期了对应时长。

#### 3.1 订单续期

!!! example "" 
    ```
    ./lambdacli tx market order-renewal [orderId] [duration] --from [account]
    ```
    
    * `[orderId]` 需要进行续期的匹配订单ID;  
    * `[duration]` 订单续期时长，单位为月。如设为3month，为续期3个月。
    
    !!! 示例
        账户`buyaccount`给自己购买的匹配订单`0D3FAE471BFC92CED2AB7806E6AC648973357CAF` 续期2个月
        ```
        ./lambdacli tx market order-renewal 0D3FAE471BFC92CED2AB7806E6AC648973357CAF 2month --from buyaccount --broadcast-mode block -y
        ```
        返回结果
        ```
        Response:
          Height: 63
          TxHash: 144EE614E02E1F4C347BEC08785A74E7F01411BEB6735FC668D25C23E078FEFD
          Raw Log: [{"msg_index":"0","success":true,"log":""}]
          Logs: [{"msg_index":0,"success":true,"log":""}]
          GasWanted: 200000
          GasUsed: 42848
          Tags:
            - action = orderRenewal
            - address = lambda1jlh7644ghjjt72quxhraxt7aegj79pdr7unczs
         
        ```

#### 3.2 矿工更新订单数据        
   订单续期后，需要执行`minernode order refresh`使矿工获取匹配订单最新结束日期
    
!!! example "" 
        
    ```
    ./minernode order refresh
    ```
    返回结果：
    ```
    Below orders have been refreshed:  1
    7A15D9D8D35B2E4BE8DAFA4DCE0F4E2B04A2F126
    ```  

#### 3.3 存储更新订单数据               
   订单续期后，需要重新执行`storagecli token sync [account]`使存储获取订单最新日期，通过`storagecli order list [account]` 可查看订单到期时间
    
!!! example "" 
        
    执行`storagecli token sync`获取订单最新日期
    ```
    ./storagecli token sync buy
    ```
    返回结果：
    ```
    Password to sign with 'buy':
    sync orders begin, This may take some time...
    http://182.91.242.11:13659/market/user/matchorders/lambda1ejuhsxthm7kpjz63eczlg28prrfje9vd22ma3x
    Order                                              Total                Used
    19FF9732F7E9069C689216173D3842612EDF02CC           6.0 GiB              101 MiB
    293B8613B1E26A79F6554472645FACB809F4BAE8           30 GiB               7.9 GiB
    29E301D07BDF6D22CE5813760F8F857326842C20           7.0 GiB              200 MiB
    5A8E65C1C04177234DC8E7B7DFBCE98CC31134AC           1.0 GiB              677 MiB
    EC349DC8803BEE33B21E487A2481EB94CFC1F8DD           5.1 GiB              627 MiB
    sync orders finish
    ```
    
    `storagecli order list` 可查看订单到期时间
    ```
    ./storagecli order list buy
    ```
    返回结果：
    ```
    Password to sign with 'buy':
    
    OrderId                                  |Expire                  |Used/Total      |ProviderStatus
    19FF9732F7E9069C689216173D3842612EDF02CC |2020-09-10 17:36:26 CST |100 MiB/6.0 GiB |Avaialable
    293B8613B1E26A79F6554472645FACB809F4BAE8 |2020-09-24 18:23:49 CST |7.9 GiB/30 GiB  |Avaialable
    29E301D07BDF6D22CE5813760F8F857326842C20 |2020-07-12 17:37:06 CST |200 MiB/7.0 GiB |Avaialable
    5A8E65C1C04177234DC8E7B7DFBCE98CC31134AC |2020-09-29 09:48:16 CST |50 MiB/1.0 GiB  |Avaialable
    EC349DC8803BEE33B21E487A2481EB94CFC1F8DD |2020-08-11 17:35:00 CST |150 MiB/5.1 GiB |Avaialable
    Total: 5
    Current time: 2020-04-14 17:58:49 CST
       
    ```

## 三、文件上传和查看

### 1. 配置

!!! example ""
    初始化storagecli
    ```
    ./storagecli init 
    ```
    初始化`storagecli` 后会默认生成配置文件`~/.lambda_storagecli/config/user.toml`

    !!! abstract ""
        
        === "修改配置"    
            ```
            ./storagecli config broker.validator_addr [nodeip]:13659
            ```
            - `[nodeip]` 为自己质押的验证节点`公网IP`
        
            ??? note "展开查看配置说明"
                ```shell hl_lines="8"
                [broker]
                # dht_gateway_addr为验证节点的dht服务 IP和端口；
                # 可以是自己质押的验证节点配置的kad.external_address
                # 可选官方dht地址：zjk.mainnet.lambdastorage.com:12000/hhht.mainnet.lambdastorage.com:12000/bj.mainnet.lambdastorage.com:12000/hk.mainnet.lambdastorage.com:12000/tokyo1.mainnet.lambdastorage.com:12000/tokyo2.mainnet.lambdastorage.com:12000
                dht_gateway_addr = "tokyo1.mainnet.lambdastorage.com:12000" 
                # validator_addr为验证节点IP和端口，可以是自己质押的验证节点rest-server服务指定的laddr地址
                # 可选官方地址：zjk.mainnet.lambdastorage.com:13659/hhht.mainnet.lambdastorage.com:13659/bj.mainnet.lambdastorage.com:13659/hk.mainnet.lambdastorage.com:13659/tokyo1.mainnet.lambdastorage.com:13659/tokyo2.mainnet.lambdastorage.com:13659
                validator_addr = "tokyo1.mainnet.lambdastorage.com:13659"   
                
                [gateway]
                # local listen address
                address = "0.0.0.0:9002"
                # for login web UI
                access_key = "accesskey"
                secret_key = "secretkey"
                ```


!!! example ""
    同步所有订单的token
    ```
    ./storagecli token sync [account-name]
    ```
    - `[account-name]` 为发起买单账户名称

  
  
### 2. 上传文件

文本/图片/视频/音频/可执行文件/压缩包文件可正常上传。上传源文件路径为绝对路径。

* `[orderId]` 为匹配订单`orderID`;
* `[account-name]` 为发起买单账户名称；
* `[bucket-name]` 可设置为长度不小于3且不大于64位的英文大小写，一个订单下可以有多个`bucket`

#### 2.1 上传文件

!!! example ""
    
    创建bucket：
    ```
    LAMBDA_ORDER_ID=[orderId] ./storagecli mb [account-name] lamb://[bucket-name]/
    ```
    
    上传文件：
    ```
    LAMBDA_ORDER_ID=[orderId] ./storagecli cp [account-name] [srcPath] lamb://[bucket-name]/ 
    
    ```
    
    注意：
    当矿池达到物理瓶颈时上传成功率会下降。
    需要分析资源瓶颈升级物理架构。
    或使用 `./storagecli config broker.disable_countersign true` 减少传输量(上传用户放弃仲裁权益)。


#### 2.2 查看上传文件列表

!!! example ""
    ```
    LAMBDA_ORDER_ID=[orderId] ./storagecli ls lamb://[bucket-name]/ 
    ```
  
  
### 3. 查看订单和矿工状态

!!! example ""
    ```
    ./storagecli order list [account-name]
    ```

    !!! 示例
        ``` 
        ./storagecli order list myaccount 
        ```
        ```
        OrderId                                  |Expire           |Used/Total      |ProviderStatus
        81B7663F9D5F40A37F4875FC1B95E2C5E1CD7FEA |2020-04-24 09:00 |100 GiB/100 GiB |Maintaining
        EF667304E33C6AAB9D56F04DF878FD93A5153B6D |2020-04-24 09:00 |100 GiB/100 GiB |Invalid
        Total: 2
        
        ProviderStatus一列为矿工状态，Avaialable为正常状态，Maintaining矿工正在维护，Invalid 矿工失效
        ```
  
  
## 四、文件分享

一个账户可以通过分享命令给另一个存储账户进行分享文件。接收者可以在分享者分享的期限内下载文件.

### 1. 分享文件
 
!!! example "" 
    用法： 
    ```
    storagecli token share ACCOUNT [remote path] [duration] --download  [flags]
    ```
    
    * `[remote path]`：分享文件的文件地址，可以分享整个文件夹，不加具体文件即可
     
    * `[duration]`：分享文件的期限，Y:年 M:月 d:天 h:小时 m:分 s:秒.（`8M7h6m`, 代表: 8个月 + 7小时 + 6分）
    
    !!! 示例
        ```
        LAMBDA_ORDER_ID=5A8E65C1C04177234DC8E7B7DFBCE98CC31134AC ./storagecli token share buy lamb://test/file50_e477d42cadc445049507f215142be187  1M2h3m4s  --download
        ```
        返回结果：
        ```
        Password to sign with 'buy':
        create share token with these properties:
        share duration: 722h3m4s
        share path: lamb://test/file50_e477d42cadc445049507f215142be187
        share type: [download]
        please wait a few seconds
        got share token secret:
        2b7nqoMMBrKzEUrvz44yFWHUk3xRpBYtvy7seKpwjVdJz2iAnhBpJMiXghhkrXLqPD
        ```
    执行命令后会输出`got share token secret`,接受者用来接收文件。
  
  
### 2. 接收分享文件

!!! example ""
    
    ```
    LAMBDA_ORDER_ID=[orderId] ./storagecli token restore ACCOUNT   [flags] 
    ```
    
    - `ACCOUNT`:接收账户
    
     
    !!! tip
        `--secret`是必填`flag`。
    
    !!! 示例
        ```
        LAMBDA_ORDER_ID=2E5A78E1564E7D220C327B1EC4F7087AD7CF2708  ./storagecli token restore teshare `--secret` 3gyjicaEhiNa8i8pighP6gbnVZLxAkqfBCQUgv9SAmQLu7453zgvyb48BzMcvouUUw  
        ```
        返回结果：
        ```
        http://182.91.242.11:13659/market/user/matchorders/lambda1ejuhsxthm7kpjz63eczlg28prrfje9vd22ma3x
        file download keys nums 1
        ```
  
  
### 3. 接收并下载分享文件

!!! example ""
    接收并下载分享文件，可以省略接收文件这一步骤。
    
    ```
    LAMBDA_ORDER_ID=[orderId] ./storagecli cp ACCOUNT [srcPath] [dstPath] [flags]
    ```
    
    - `ACCOUNT` :接收账户
    * `[srcPath]` ：下载文件地址
    * `[dstPath]`：下载后放文件地址
    
    !!! tip
        `--secret`是必填的`flag`。
        
    !!! 示例
        ```
        LAMBDA_ORDER_ID=2E5A78E1564E7D220C327B1EC4F7087AD7CF2708 ./storagecli cp  teshare lamb://test/testfiles.tar.gz_414c7b9aa8154c268220d93a8b8a131f  /root/qwe/ `--secret` 3gyjicaEhiNa8i8pighP6gbnVZLxAkqfBCQUgv9SAmQLu7453zgvyb48BzMcvouUUw
        ```
        返回结果：
        ```  
        http://182.91.242.11:13659/market/user/matchorders/lambda1ejuhsxthm7kpjz63eczlg28prrfje9vd22ma3x
        file download keys nums 1
        duplicate token.
        found only one candicate
        downloading testfiles.tar.gz_414c7b9aa8154c268220d93a8b8a131f
        492347394 / 492347392 [---------------------------------------------------------------------------------------------------------------------------------------------------] 100.00% 12099253 p/s
        download done 410289495
        ```
        
### 4. 下载分享文件

!!! example ""
    下载分享文件需要先接收分享文件，再下载分享文件。
    
    用法：
    ```
    LAMBDA_ORDER_ID=[orderId] ./storagecli cp ACCOUNT lamb://[bucket-name]/  [srcPath] [flags]
    ```
    
    * `ACCOUNT` :接收账户
    * `[srcPath]` ：下载文件地址
    
    !!! 示例
        ```
        LAMBDA_ORDER_ID=92F1918765F3654EE1E4F98BD64B96CB4DD4C0BC  ./storagecli cp  teshare lamb://test/upload.tar.gz_3484a737e325439b80ef79cb1297d3a2  /root/qwe/ 
        ```
        返回结果：
        ```
        found only one candicate
        downloading upload.tar.gz_3484a737e325439b80ef79cb1297d3a2
        1400395776 / 1400395752 [-------------------------------------------------------------------------------------------------------------------------------------------------] 100.00% 11287511 p/s
        download done 1166996480
        ```

## 五、挖矿
### 1. 矿工挖矿

矿工每接受文件`8GB`文件会对应生成一个声明，所有声明有效期为1个月，每个出块周期（大约每6s出一个块）会由共识网络发起挑战，挑战声明成功并提交挖矿证明的矿工就会得到一笔收益。


1. 有有效声明的矿工有挖矿权利；
2. 矿工已存文件每满8G可生成1个声明；
3. 单个矿工声明越多，该矿工被挑选到的概率越大。


### 2. 挖矿收益
矿工收益 = 单个区块增发量 * （43% * 95% / 挖矿的矿工数量） + 单个区块增发量 * （43% * 5% / 挖矿的矿工数量 ）* 矿工质押量在节点质押量的占比 * 75%

```
比如单个区块增发量为100LAMB，全网共1个节点该节点质押666TBB，全网共10个矿工分别质押1TBB且分别有10个声明。
则单个矿工单个区块得到的挖矿奖励为4.085LAMB= 100LAMB * 43% * 95% / 10 + 100LAMB * 43% * 5% / 10 * 1/676 * 75%
```

## 六、提取订单收益
[提取单个匹配订单收益](lambdacli/tx/market/withdraw-miner.md)  
[批量提取匹配订单收益](lambdacli/tx/market/miner-withdraw-count.md)

## 七、测试网络连通

当启动`miner`、`storagenode`、或上传文件时有报错，请使用以下命令进行排查。

### 1. 测试miner服务
```
./minernode info --test
```

!!! success "返回如下结果"
    ```
    
                   version: 0.2.7.1
                    dht id: G4xW3UHMfFnTmaRMZUJ7PKcfvr9YTTFyekcsRxKDZZD9
    server.private_address: 172.11.159.11:15001   successful
            server.address: 0.0.0.0:26654    successful
      kad.external_address: 39.106.153.11:26654    successful
        kad.bootstrap_addr: [39.106.153.11:26650 172.11.159.11:26652]    successful successful
          Ensure-level = 0: 1/6 of disk-space would be used for data-replicating
    ```
### 2. 测试storagenode服务
```
./storagenode info network --test
```

!!! success "返回如下结果"
    ```
                   version: 0.2.7.1
                    dht id: 3mta4YEgHB43RHYE83aWBouvFNNCtSc832siEwmcTUsZ
      storage.storage_name: sn1
     storage.miner_address: 172.11.159.11:15001   successful
    server.private_address: 172.11.159.11:16001   successful
            server.address: 0.0.0.0:26660    successful
      kad.external_address: 39.106.153.11:26660    successful
        kad.bootstrap_addr: [172.11.159.11:26650 172.11.159.11:26652]     successful successful 
    ```

### 3. 查看存储节点磁盘空间
```
./storagenode info disk
```

!!! success "返回如下结果"
    ```
                   version:  0.2.7.1
      storage.storage_name:  sn1
          storage.data_dir:  [/lambda/data/xvdd/store /lambda/data/xvde/store /lambda/data/xvdc/中文test/store /lambda/.1lambda_storage/store]

    Disk                           |Total  |Used    |Free    |Order                                    |Reserved |Occupied
    /lambda/data/xvdd/store        |18 GiB |8.9 GiB |8.8 GiB |753E54547CC66DB840E6C717C98492640B6E5CF8 |3.0 GiB  |540 MiB
                                   |       |        |        |E15F0CCA09A8F92E401E322638CA777BC9EA24B8 |3.0 GiB  |1.9 GiB
    /lambda/data/xvde/store        |18 GiB |592 MiB |17 GiB  |D3280F0343112CC35B864CFFEE96DE3D2F39F3C7 |12 GiB   |579 MiB
    /lambda/data/xvdc/中文test/store |18 GiB |13 GiB  |4.6 GiB |DBE8C6D465D1701E71A7CBDF35E9F602A9CE55AE |6.0 GiB  |3.8 GiB
    
    Reserved为订单预留的磁盘空间，Occupied为当前订单实际占用磁盘空间
    ```

## 八、备份和恢复存储文件
以防配置文件丢失，请提前做好文件备份：[存储网络文件备份](StorageFile-Backup.md)



