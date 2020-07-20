# FAQ

### 程序版本不对
检查是否是最新版本程序
```
incompitable: Peer is on a different network. Got lambda-chain-xx, expected lambda-chain-xx.
```

### 已经Lambda程序在运行
先停止已经在运行的程序，再重新运行
```
ERROR: couldn't create db: Error initializing DB: resource temporarily unavailable.
```

### 重新升级报错
重新升级时，使用`./lambda unsafe-reset-all`清除历史区块数据  
重新启动仍然报以下错误，则检查`~/.lambda/data`目录下文件是否清除干净 
```
panic Tendermint stat.AppHash does not match AppHash after replay. Got xxxxxxxxxxxxxx, expected xxxxxxxxxx.
```

```
ls -l  ~/.lambda/data  
```
保留priv_validator_state.json，删除application.db文件.
```
drwxr-xr-x  11 xxxxxx  staff  352 Sep 15 08:57 application.db
-rw-------   1 xxxxxx  staff   48 Sep  8 23:23 priv_validator_state.json
```

### 查询验证节点公钥是否丢失

```
./lambdacli query tendermint-validator-set | grep Pubkey | grep `./lambda tendermint show-validator`
```

### 查询节点同步块高
```
./lambdacli status | grep --color latest_block_height
```

### 查询节是否正常参与投票
下载lambda-debugtool
```
wget https://github.com/LambdaIM/lambda-debugtool/releases/download/v0.0.1/lambda-debugtool.tar.gz
tar zxvf lambda-debugtool.tar.gz
```
1. 查询原始签名公钥
```
./lambdadg show --pubkey `./lambda tendermint show-validator`

```
2. 查询最新出块高度
```
curl http://localhost:26657/status
```
3. 查询最新出块api投票
在当前接口的返回json，precommits内是否包含节点的原始签名私钥
```
curl http://localhost:26657/block?height=区块高度
```

### 节点成为无效节点(被jail)
当节点对块进行双签，在最近的10000个块中对少于500个块签名会被jail，并扣除少量tbb.

##### 重新加入共识网络
发起unjail消息来重新加入共识网络 被jail之后的节点需要等待10分钟的惩罚来发起unjail命令  
```
./lambdacli tx slashing unjail --from [your-account-name] --broadcast-mode block
```

##### 自抵押不足
如果不满足validator的最低质押要求666,666,666utbb, 需要发起质押补足扣除的utbb  
```
validator's self delegation less than MinSelf Delegation, cannot be unjailed
```

### 查询账户不存在？

出现如下错误提示, 可能是由于您刚刚启动 lambda 还没有同步到最新块高
可以通过日志(`/tmp/lambda.log`)查看块高情况
```
[root@zh]# ./lambdacli query account lambda1z66gxs2wlhmkhh3rljtkzk96fqkk7809zb123
ERROR: {"codespace":"sdk","code":9,"message":"account lambda1z66gxs2wlhmkhh3rljtkzk96fqkkl7809zb123 does not exist"}
```

### ABCI 连接被拒绝？
出现如下错误提示，可通过`telnet`命令检查您的机器 26656 和 26657 端口是否能通
```
ERROR: ABCIQuery: Post xxx connect: connection refused
```

### 如何修改 Validator 名称
```
./lambdacli tx staking edit-validator --moniker "your-custom-name" --from [your-account-name] --broadcast-mode block -y
```

### 执行lambdacli keys 子命令报错
如果执行lambdacli keys相关子命令报错有以下报错  
`ERROR: couldn't create db: Error initializing DB: leveldb: manifest corrupted (field 'comparer'): missing [file=MANIFEST-xxxxxx]`

则执行`./lambdacli keys repair`后再执行 lambdacli keys 相关子命令看返回结果是否正常

### 备份和恢复节点签名文件
参考：[备份和恢复节点签名文件](Mainnet-Validator-Keybackup.md)

### 单位换算

UINTS|  CONVERSION |
-----|-------------|
TBB/LAMB| 1 : 3000 
utbb/ulamb| 1 : 3000
TBB/utbb| 1 : 10<sup>6</sup> (100万)
LAMB/ulamb|1 : 10<sup>6</sup> (100万)
TBB/ulamb|  1 : 3 * 10<sup>9</sup> (30亿)
节点最少质押666.666666TBB|  666.666666TBB = 1999999.998LAMB = 666666666utbb = 1999999998000ulamb
矿工最少质押1TBB|  1TBB = 3000LAMB = 1000000utbb = 3000000000ulamb
