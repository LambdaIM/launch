# 挖矿
## 挖矿环境
### 矿机配置
CPU：4核+  
内存：8G+  
带宽：5M+(有公网IP)  
磁盘：1T+  


### 环境管理
主网新矿工和存储节点接入参考：[配置矿工和存储节点](Mainnet-Miner-Guide.md) 
测试网新矿工和存储节点接入参考：[配置矿工和存储节点](Testnet-Miner-Guide.md)

#### 查看配置
```
./storagecli   config
./lambdacli    config
./storagenode  info disk
./storagenode  info network
./minernode    info
```
#### 检查网络步骤
1. 检查是否开启防火墙
2. 检查端口映射是否成功
3. 检查配置是否正确

#### 测试网络配置
```
./minernode   info --test
./storagenode info network --test
```
#### 多磁盘配置
```
#～/.lambda_storage/config/config.toml
[storage]
data_dir = [ "磁盘1", "磁盘2", "磁盘N"]
```

#### 多存储节点配置
```
# 与单节点配置相同
# miner node自动分配存储节点进行存储
```
#### 查看存储节点
```
./minernode storage list
```
#### 查看订单使用空间
```
./storagenode info disk
```

## 存储挖矿
### 存储架构
![avatar](img/store/storestructure.png)

### 网络架构
![avatar](img/store/netstructure.png)

### 挖矿子帐户
用途：minernode提交挖矿声明、挖矿证明交易

生成方式：钱包、lambdacli创建挖矿子帐户

### 挖矿过程
1. 提交挖矿声明  
   矿工每存储8GB数据会封装1个挖矿声明  
   1挖矿声明 = 8存储算力  
  
2. 挖矿声明有效期  
   挖矿声明有效期默认为1个月，过期后会自动重新提交  
   挖矿声明有效期 < 存储订单有效期  
   矿机存储A订单，A订单有效期为1个月，挖矿声明有效期为1个月  
   矿机存储A、B订单，A有效期1个月、B有效期6个月，挖矿声明有效期1个月  
   矿机存储A、B订单，A有效期3个月、B有效期6个月，挖矿声明有效期3个月  
   当A订单数据过期后可释放A订单占用空间，B订单数据会重新封装声明  
   用户的存储订单可在最大购买时间(--max-buy-duration)内进行续期  
  
3. 提交挖矿证明  
   每个区块选择1名矿工提交挖矿证明，存储算力越大被选中概率越高  
   挖矿证明需要在5个区块周期内提交  
  
4. 获得出块奖励  
   出块奖励的43% 给提交挖矿证明的这名矿工  
   建块验证节点收取打包挖矿证明的5%手续费  
   矿工未提交挖矿证明则该笔奖励打入销毁池   

### 矿工维护
矿工因升级或其他理由需要暂时停止提供服务时，可执行矿工维护命令 使矿工进入维护状态。矿工维护完成后，可执行解除维护命令 恢复活跃。

1. 区块链内最多允许21个矿工同时进行维护；  
2. 30天内，单个矿工累计维护时长不允许超过3天；  
3. 30天内，如矿工累计维护时长超过3天，矿工会被监禁； 
4. 超过5000次未成功响应挑战，矿工会被监禁；
5. 被监禁的矿工，可使用`lambdacli tx market unjail`解禁，同时会扣除矿工账户余额100LAMB。

操作文档参考：[矿工维护手册](Lambda-Miner-Maintain.md)

### 匹配订单续期
区块链支持匹配订单续期功能。   
1. 匹配订单未到期的，购买了空间的账户可使用`lambdacli tx market order-renewal`命令续期。  
2. 匹配订单已过期的，不能再进行续期；  
3. 同一匹配订单可多次续期；  
4. 续期后的匹配订单总时长（即结束时间减开始时间），不能超过60个月（1个月=30天)；  
5. 订单续期后，需要执行`minernode order refresh`使矿工获取匹配订单最新结束日期；  
6. 订单续期后，需要重新执行`storagecli token sync [account]`使存储获取订单最新日期            

操作文档参考：[匹配订单续期](http://docs.lambda.im/Mainnet-Miner-Guide/#3_1)

# 常见问题
## 上传文件报错
检查网络环境是否正确

检查存储节点、矿工节点日志是否有报错信息，并反馈给项目维护人员

### 挖矿成功率为0%
1.检查矿工是否被监禁  
``` 
检查矿工状态命令:  
./lambdacli query market miner [miner_address]  
解除监禁命令:  
./lambdacli tx market unjail --from [miner_account]
```  
操作文档参考：[矿工维护手册](Lambda-Miner-Maintain.md)

2.检查存储订单是否过期  
``` 
检查匹配订单命令:
./lambdacli query market matchorders [account_address] [page] [limit]
订单续期命令：  
./lambdacli tx market order-renewal [orderId] [duration] --from [account]
``` 
操作文档参考：[匹配订单续期](http://docs.lambda.im/Testnet-Miner-Guide/#3_1)    

3.检查minernode与storagenode网络是否正常  
``` 
    ./minernode   info --test  
    ./storagenode info network --test  
```

4.检查矿工节点和存储节点程序是否正在运行，是否有错误日志信息

5.检查订单使用空间

```
检查订单使用空间命令：
./storagenode info  disk  --local-mode   
               version:  0.2.7_rc2-13-gdbcabcf-debug
  storage.storage_name:  t4s5
      storage.data_dir:  [/data2/storage/store /data3/storage/store /data/storage/store /data4/store]

Disk                 |Total   |Used   |Free    |Order                                    |Occupied |SafeCleanup?
/data2/storage/store |18 GiB  |14 GiB |4.6 GiB |0A0250B4143BD1F69DFBEBD98ADDDFEF99397511 |240 MiB  |false
                     |        |       |        |82EB03450C809F3F8867C8D30BDD42D6C8802E92 |2.7 GiB  |false
/data/storage/store  |187 GiB |23 GiB |164 GiB |82EB03450C809F3F8867C8D30BDD42D6C8802E92 |3.3 GiB  |false
                     |        |       |        |BB549FB804062AB89A6AE3C3C8B6E1188EA9F36C |128 MiB  |false
                     |        |       |        |F083BC34E5CC1E2E6DBD20F0A274A70252DCCBC3 |1.3 GiB  |false

```

6.清理过期订单空间
```
清理过期订单空间命令：
—safe-clean会把SafeCleanup的值为true的订单删除并且不影响挖矿/算力

./storagenode info  disk  --safe-cleanup 
             blockTime:  2020-04-12 14:01:27 UTC
               version:  0.2.7_rc2-13-gdbcabcf-debug
  storage.storage_name:  t4s5
      storage.data_dir:  [/data2/storage/store /data3/storage/store /data/storage/store /data4/storage/store]

Disk                 | Total   |Used   |Free    |Order                                    |Occupied |SafeCleanup?
/data2/storage/store |18 GiB  |14 GiB |4.6 GiB |0A0250B4143BD1F69DFBEBD98ADDDFEF99397511 |240 MiB  |false
                     |        |       |        |82EB03450C809F3F8867C8D30BDD42D6C8802E92 |2.7 GiB  |false
/data3/storage/store |18 GiB  |18 GiB |0 B     |A60DF26061D0A98D4F9338AAC8A0683BD0927429 |18 GiB   |true
/data/storage/store  |187 GiB |50 GiB |136 GiB |51866A6BBB6E2EE819D921D85094E76D1D54410A |116 MiB  |true
                      |        |       |        |82EB03450C809F3F8867C8D30BDD42D6C8802E92 |3.3 GiB  |false
                      |        |       |        |BB549FB804062AB89A6AE3C3C8B6E1188EA9F36C |128 MiB  |false
                      |        |       |        |F083BC34E5CC1E2E6DBD20F0A274A70252DCCBC3 |1.3 GiB  |false
/data4/storage/store  |37 GiB  |34 GiB |2.7 GiB |A60DF26061D0A98D4F9338AAC8A0683BD0927429 |7.0 GiB  |true
```

7.矿工成交订单处理

挖矿过程中，矿工需要定期对成交的订单发起提现操作，以保证矿工账户中有足够的lamb。
如果发现匹配的订单已经过期，此时需要对成单发起提现操作，否则可能会
影响矿工整体的可用空间，影响创建卖单。

使用`./lambdacli query market matchorders [acc] [page] [limit]`查询成单，观察`EndTime`字段，
如果有`EndTime`小于当前时间的订单，需要对该成单进行提现，或者使用批量提现功能。

单笔提现：`lambdacli tx market withdraw-miner [matchOrder-id] --from master --broadcast-mode block -y`

批量提现：`./lambdacli tx market miner-withdraw-count [page] [limit] --from acc --broadcast-mode block -y`

*注：如果批量提现返回gas错误，需要指定gas数量，使用`--gas [count]`, count最大可设置为4000000，可保证提现成功。*

