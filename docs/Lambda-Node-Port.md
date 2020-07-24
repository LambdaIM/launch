# Lambda端口说明

### 节点端口
`26656` p2p通讯端口  
`26657` tendermint默认的rpc接口端口  
`13659` lambda的rpc端口，主要是查询相关业务   
`12000` 验证节点dht端口   

### 矿工端口 
`13000` 矿工服务端口  
`14000` 存储服务端口

### 矿工切换验证节点
如果当前链接的验证节点慢，可切换其他验证节点
```
./lambdacli config node tcp://[nodeip]:26657
```  
        
- `[nodeip]` 为需要更换的验证节点`公网IP`

### 节点恢复状态
1. 节点进程异常停止后，如启动节点日志报错`Wrong Block.Header.AppHash.  Expected XXX, got XXX`  
解决：  
可在启动命令后加上`--replay-last-block`参数，修复状态并启动：
``` 
./lambda start --p2p.laddr tcp://0.0.0.0:26656 --rpc.laddr tcp://0.0.0.0:26657 --daemonize --log.file /tmp/lambda.log --replay-last-block
```


2. 节点进程异常停止后，如启动节点日志报错`pdp module db's version is different from app db's version: appDB=xxx moduleDB=xxx zeroVersion=0, please use lambda state fix recovery store state`  
解决：  
使用`./lambda reset --height [height]`，再启动节点即可  
此处`height`需要比`appDB`和`moduleDB`中较小那个数值小一个块高

例如报错：
```
pdp module db's version is different from app db's version: appDB=15333 moduleDB=15297 zeroVersion=0, please use lambda state fix recovery store state
``` 
修复：  
`./lambda reset --height 15296`  
（appDB=15333，moduleDB=15297，moduleDB比appDB小，设定块高需要比moduleDB小1）

启动节点：
``` 
./lambda start --p2p.laddr tcp://0.0.0.0:26656 --rpc.laddr tcp://0.0.0.0:26657 --daemonize --log.file /tmp/lambda.log 
```







