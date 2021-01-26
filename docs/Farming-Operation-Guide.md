# 聚合挖矿市场操作手册

## 聚合挖矿市场说明
具体参考：[Lambda 聚合协议技术原理](Poly-Mining-Protocol.md)  

1. 新增聚合挖矿市场，用户可以向聚合挖矿市场存入资金（不少于10000LAMB），享受挖矿收益分成

3. 矿工可以声明挖矿到聚合挖矿市场，只需要缴纳一小部分按照挖矿空间计算的手续费（0.3%），矿工接受文件生成声明（每8GB一个声明）后就可以参与挖矿并且享受挖矿收益分成

4. 用户可以随时提取收益，用户的收益是根据矿工收益情况来计算，每次结算需要整个聚合挖矿市场用户存入金额有变化才会触发

5. 矿工也可以随时提取收益，只是挖矿收益只有25%会立刻释放，剩下75%进行线性释放


## 聚合挖矿用户
### 存入资金

任意`ulamb`持有者可以存入资金到聚合挖矿市场，当前最小提供金额为`10000000000ulamb`（10000LAMB）

```
./lambdacli tx pool supply 10000000000ulamb --from [account]
```

说明
```
用户可以无限制的提供一定量的tokens给池子，并且每次提供，系统会根据之前的用户提供tokens比例结算之前一段时间的收益，并且重新更新用户的质押比例
```

### 取消存入资金

已经存入资金的用户可以取消一部分资金，当前最小取消金额为`10000000000ulamb`

```
./lambdacli tx pool abort 10000000000ulamb --from [account]
```

### 提取奖励

用户可以从聚合挖矿市场提取分成的挖矿收益

```
./lambdacli tx pool withdraw --from [account]
```

**注意**

用户可以提取部分的收益并不是实时结算的，而是在整个聚合挖矿市场的用户质押比例有变化的时候进行结算

## 聚合挖矿矿工
账户质押TBB并`create-miner`成为矿工后，可进入lambda市场或聚合挖矿市场进行挖矿。  
矿工初始化及存储配置参考：[矿工0.3.2接入教程](Testnet-Miner-Guide.md)

**注意**

lambda市场的矿工不可以在聚合挖矿市场声明挖矿，同理，聚合挖矿市场的矿工也不可以在lambda市场进行挖矿

### 声明挖矿空间

1. 矿工可在聚合挖矿市场中声明挖矿且无需任何保证金，只需要按挖矿空间比例支付一笔小额手续费即可；
2. 声明挖矿空间的矿工会自动生成一笔类似普通市场的匹配订单，可使用该订单上传下载文件

```
./lambdacli tx pool declare-mining --size [size]GB --from [miner-name]
```

- `size` 声明挖矿的空间，单位为GB

说明：矿工在声明挖矿时候，需要提交一笔手续费，这笔手续费的计算相当于空间对应LAMB的兑换比例
```
例如：
某个矿工在聚合挖矿市场声明一笔1000G的挖矿空间需要9LAMB手续费

./lambdacli tx pool declare-mining --size 1000GB --from miner2
则手续费的计算为:
1000GB = 1TB 相当于1个TBB，
当前1TBB兑换1LAMB的比例为3000
fee = 1 * 3000(兑换比例) * 0.3%(手续费比例) = 9LAMB (=9,000,000ulamb)
```

### 查询匹配订单

!!! example ""  
    查询账户地址：
    ```
    ./lambdacli keys show [account-name] --address
    ```
    根据账户地址查看匹配订单：
    ```
    ./lambdacli query pool match-orders [address] [page] [limit]
    ```
        
    !!! 示例    
        ```
        ./lambdacli keys show buyaccount --address
        ```
        返回结果：`lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr`
        ```
        ./lambdacli query pool match-orders lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr 1 10
        ```
        返回结果：
        ```shell hl_lines="2 9 10"
        MatchOrder
          OrderId:               A8C4171BB10217BB1DBB029C5176FC1D12ABFA53#匹配订单ID，上传文件时需要用到该ID
          AskAddress:            lambdamineroper1k6rxrmly7hz0ewh7gth2dj48mv3xs9yznx96fn
          BuyAddress:            lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr
          SellOrderId:
          BuyOrderId:
          Price:                 0
          Size:                  200
          CreateTime:            2021-01-25 03:29:49.951830374 +0000 UTC #匹配订单开始时间
          EndTime:               2021-02-24 03:29:49.951830374 +0000 UTC #匹配订单结束时间
          CancelTimeDuration:    0s
          WithDrawTime:          2021-01-25 03:29:49.951830374 +0000 UTC
          Status:                0
          MarketAddress:         lambdamarketoper1yl9v25pcxem9e5g828f84d9xu97h4qx5p667tp
          UserPay:               0ulamb
          MinerPay:              0ulamb
          PeerId:
          DhtId:                 7x5eUjiEnGX23LK6cTYqEL1JYWbLRFtqYUxyzrnBF8s1
        ```

### 取消挖矿

矿工可以取消已经过期的挖矿订单来赎回空间

```
./lambdacli tx pool mining-abort [orderID] --from [account]
```

### 提取挖矿收益

矿工可以发起交易提取挖矿收益，提取部分为已经释放的挖矿收益

```
./lambdacli tx pool mining-withdraw --from [account]
```

说明
```
当前矿工在获取收益的时候，每次只有25%会立刻释放，其他75%会按照时间线性释放
```

### 挖矿订单续期

矿工可以对未过期的挖矿订单进行续期，每次默认的续期时长为1个月，且不能对离到期时间大于一个月的订单重复操作(防止无限期续期)

```
./lambdacli tx pool order-renew [orderID] --from [account]
```
订单续期后，需要执行`minernode order refresh`使矿工获取匹配订单最新结束日期；  
订单续期后，需要重新执行`storagecli token sync [account]`使存储获取订单最新日期 








