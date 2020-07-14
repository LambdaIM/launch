# 数字资产和市场操作手册

任意账户可创建数字资产和资产市场；  
矿工可质押数字资产参与挖矿，瓜分资产市场每块增发币数量。  

## 资产挖矿
### 资产矿工
1. 按所有矿工单个资产下算力排序，算力前50的矿工会进入对应资产大矿工列表，其余矿工为小矿工；
2. 每个区块在大矿工列表中选择5名矿工提交挖矿证明，存储算力越大被选中概率越高；
3. 小矿工每10000块至少提交一次证明，每10000块最多提交100次提交证明；
4. 超过5000次未成功响应挑战，大矿工会被监禁；
5. 小矿工每10000块内未提交自挑战证明，扣除该周期内5%的收益；累计到100000块未提交，累计扣除该矿工50%的收益；
6. 小矿工累计100000块未提交自挑战证明，节点可使用`./lambdacli tx dam deactivate`命令移除资产矿工，节点可获得扣除收益的5%，其余扣除收益烧毁；
7. 矿工被移除后不能再提交资产声明和证明，也无法获得挖矿奖励。可使用`./lambdacli tx dam miner activate`命令激活，重新参与挖矿获得奖励。

操作文档参考：
[资产矿工操作命令](lambdacli/tx/dam/miner.md)

### 资产挖矿过程
1. 提交资产挖矿声明  
   矿工每存储32GB数据会封装1个资产挖矿声明  
   1挖矿声明 = 32存储算力  
  
2. 资产挖矿声明有效期  
   挖矿声明有效期默认为7天，过期后会自动重新提交    
   用户的存储订单可在有效期时间内进行续期  
  
3. 提交资产挖矿证明  
   按所有矿工资产算力排序，算力前50的矿工会进入资产大矿工列表
   每个区块在大矿工列表中选择5名矿工提交挖矿证明，存储算力越大被选中概率越高  
   资产挖矿证明需要在5个区块周期内提交  
  
4. 获得出块奖励  
   每块对 5 名大矿工进行挑战，出块奖励的 60% 给这 5 名大矿工平分，大矿工未提交挖矿证明则该笔奖励打入销毁池，未被挑战到的大矿工此块不参与奖励；其余奖励剩余小矿工平分。    



### 创建数字资产
1. 创建数字资产需要消耗账户1000000LAMB(1LAMB=1000000ulamb) 。
2. 创建资产成功后，预留数量资产会直接进入创建者账户。
3. 资产发行总量需要小于等于900亿  

```
 ./lambdacli tx asset create [amount+symbol] 1000000000000ulamb \
--asset-name [asset-full-name] \
--mint-type inflated_mint \
--total-supply [total-supply] \
--inflation [inflation] \
--adjust-rate [adjust-rate] \
--adjust-period [adjust-period] \
--max-adjust-count [max-adjust-count] \
--genesis-height [genesis-height] \
--from [account]
```
- `[amount+symbol]` 为创建数字资产的预留数量和资产名称；预留数量不能超过发行总量，资产名称必须以字母`u`开头；创建资产成功预留数量资产会直接进入创建者账户
- `[asset-full-name]` 为资产全称，支持中英文及其他任意字符。
- `[mint-type]`  增发类型，可设置为`not_mint`（不可增发）、`one_time_mint`（一次性增发）、`inflated_mint`（块增发）。其中`inflated_mint`用于挖矿增发。  
- `[total-supply]`  指定发行的资产总量。  
- `[inflation]`  为初始每块增发资产数量。
- `[adjust-rate]`  为资产增发数量减产系数，需要小于1。  
- `[adjust-period]`  为每个减产周期出块数量。  
- `[max-adjust-count]`  为最大减产次数。  
- `[genesis-height]`  为初始挖矿块高。区块链到指定块高后，有资产矿工提交声明和证明，资产才会增发，否则不增发。     

例如：
```
需要创建uxxb资产（账户余额要保证有100w LAMB，用于创建资产），
预留1亿 XXB（=100000000000000uxxb, 1XXB=1000000uxxb）资产，
指定从第50000块高（genesis-height）开始挖矿增发（50000块高以前不增发），
每块增发1000000uxxb（inflation），增发10000块（adjust-period）后，
根据减产系数（adjust-rate）调整每块增发数量为500000uxxb（=1000000uxxb * 0.5），按此数量再增发10000块，
以此类推，第二次调整增发数量为250000uxxb，第三次调整增发数量为125000uxxb，第四次调整增发数量为62500uxxb，
到第五次（max-adjust-count）调整增发数量为31250uxxb后，不再调整增发数量，每块按31250uxxb增发直到总资产数量达到发行资产总量（total-supply）900亿XXB

./lambdacli tx asset create 100000000000000uxxb 1000000000000ulamb \
--asset-name "XBB Coin" \
--mint-type inflated_mint \
--total-supply 90000000000000000 \
--inflation 1000000 \
--adjust-rate 0.5 \
--adjust-period 10000 \
--max-adjust-count 5 \
--genesis-height 50000 \
--from mykey
```
[创建数字资产](lambdacli/tx/asset/create.md)

## 资产市场

### 创建资产市场
1. 数字资产的创建人，才可以创建资产市场。
2. 创建资产市场，需要消耗100w LAMB 。

```
 ./lambdacli tx dam market create [market-name] [asset] [exchange-ratio] --from [account]
```
- `[market-name]` 为资产市场名称，支持中英文及其他任意字符。  
- `[asset]` 为资产名称。  
- `[exchange-ratio]`  为新资产兑换utbb比率，矿工质押资产空间时需要根据此值质押对应数量资产。   

例如：
```
资产uxxb的创建人，创建一个名字为market-uxxb的资产市场，兑换比率（exchange-ratio）为10，即10uxxb=1utbb。

./lambdacli tx dam market create market-uxxb uxxb 10 --from mykey --broadcast-mode block -y 

说明：
在lambda市场，1TB（=1000GB）空间需要质押1TBB（=1000000utbb），即1GB空间对应质押1000utbb。
在资产市场，矿工质押1GB资产空间，也需要质押等价于1000utbb的数字资产，即10000uxxb（=1000 * exchange-ratio）。

```
[创建数字资产市场](lambdacli/tx/dam/market.md)

### 矿工质押资产空间
1. 矿工可质押数字资产参与挖矿，瓜分资产市场每块增发币数量。
2. 质押的资产数量根据空间和市场兑换比率计算，质押成功后从矿工账户扣除对应资产数量
 
```
./lambdacli tx dam miner pledge [asset] [size] --order-price [order-price] --from [acount]
```
- `[asset]` 为资产名称。  
- `[size]`  为资产挖矿空间大小，单位为GB。
- `[order-price]`  为资产空间单价，单位为资产名称；空间价格不能低于`1000000[asset]`；仅第一次质押时设置的价格有效。

例如：
```
矿工对uxxb类型资产进行挖矿，挖矿空间2T(=2000GB)，设置空间价格为1XXB（=1000000uxxb）

./lambdacli tx dam miner pledge uxxb 2000GB --order-price 1000000uxxb --from myminer --broadcast-mode block -y 

说明：
在资产市场，矿工质押1GB资产空间，需要质押等价于1000utbb的数字资产。
假设资产市场兑换比率为10，则10uxxb=1utbb，矿工每质押1GB空间需要
10000uxxb。
所以挖矿2T空间，需要质押20XXB(= 20000000uxxb =2000 * 1000 * 10）

```

[矿工质押](lambdacli/tx/dam/miner.md)

### 购买资产空间
用户购买矿工的资产空间：
```
./lambdacli tx dam user buy --duration [duration] --size [size] --ask-address [miner-opraddr] --asset [asset] --from [account]
```

例如：
```
用户购买矿工lambdamineroper10gat77jd5ucz7gw0m3xac8jfj5l83r6c0mswdj的300GB资产空间，时长2个月
假设矿工设置资产空间单价为1XXB/GB/month(=1000000uxxb/GB/month)，用户需要花费600XXB（=600000000uxxb = 1000000uxxb/GB/month * 300GB * 2month)

./lambdacli tx dam user buy --duration 1month --size 100GB --ask-address lambdamineroper10gat77jd5ucz7gw0m3xac8jfj5l83r6c0mswdj --asset uxxb --from buyaccount

```
资产空间上传步骤与lambda市场空间文件上传步骤一致，此处不再赘述。
[文件上传和查看](http://docs.lambda.im/Testnet-Miner-Guide/#_4)

### 资产订单续期
``` 
./lambdacli tx dam user --home /lambda/tmp_behave/cli renew 91292FB3CDF43325BFF6FA68811C75968BF8CF75 1month --from genesis --broadcast-mode block -y
```

### 提取单个资产订单收益
``` 
./lambdacli tx dam miner withdraw [matchOrder-id] --from [account]

如：
先用矿工地址查询匹配订单：
./lambdacli query --home /lambda/tmp_behave/cli dam all-match-orders lambda14chzwvsh5y4yt489ea3vqelq3rpf6t839m6z85 1 100
返回结果：
Dam MatchOrder
  OrderID:               F03EFA6FB9181A960EED6D425CB9FBB6791F7B84 //匹配订单ID
  Asset:                 unnb1
  BuyAddress:            lambda1ymms062l3v55tyfkeqp605psvdh4za78k6ufcw
  AskAddress:            lambdamineroper14chzwvsh5y4yt489ea3vqelq3rpf6t8335k9jf
  DhtID:                 FF7Gqry6MvN7TcYNAtwsMvcTpCwkG4GRMFYPpuK8ur8w
  Price:                 1000000
  Size:                  100
  CreateTime:            2020-07-13 02:05:02.033907459 +0000 UTC
  EndTime:               2020-08-12 02:05:02.033907459 +0000 UTC
  WithDrawTime:          2020-07-13 02:05:02.033907459 +0000 UTC
  UserPay:               100000000unnb1

根据匹配订单ID提取订单收益：
./lambdacli tx dam miner withdraw F03EFA6FB9181A960EED6D425CB9FBB6791F7B84 --from myminer --broadcast-mode block -y
```
[资产矿工操作命令](lambdacli/tx/dam/miner.md)


### 批量提取资产订单收益
``` 
./lambdacli tx dam miner withdraw-count [asset] [page] [limit] --from [account]

如：
./lambdacli tx dam miner withdraw-count uxxb 1 100 --from myminer --broadcast-mode block -y
```
[资产矿工操作命令](lambdacli/tx/dam/miner.md)

### 查询矿工挖矿收益

```
./lambdacli query distr miner-rewards [miner-opraddr]

如：
先查询矿工操作地址：
./lambdacli keys show myminer --address --bech miner
返回结果：
lambdamineroper1g74gwkeq2py5zypv4l223p2s82gqlc28rsp826 

使用操作地址查询奖励：
./lambdacli query distr miner-rewards lambdamineroper1g74gwkeq2py5zypv4l223p2s82gqlc28rsp826
```

[查询矿工挖矿收益](lambdacli/query/distr/miner-rewards.md)

### 提取挖矿收益
矿工提取全部挖矿收益：
```
./lambdacli tx distr withdraw-miner-rewards --from [account]

如：
./lambdacli tx distr withdraw-miner-rewards --from myminer --broadcast-mode block -y
```
[提取挖矿收益](lambdacli/tx/distr/withdraw-miner-rewards.md)


### 资产赎回
1. 只能一次性赎回全部资产。
2. 矿工没有资产匹配订单，或订单已到期且订单收益全部提取完才可赎回；
3. 赎回后七天，资产返还到原账户；
4. 赎回十四天内，矿工不可以重新质押资产参与挖矿。
```
./lambdacli tx dam miner refund [asset] --from [account]

如：
./lambdacli tx dam miner refund uxxb --from myminer --broadcast-mode block -y
```

[资产赎回](lambdacli/tx/dam/miner.md)

