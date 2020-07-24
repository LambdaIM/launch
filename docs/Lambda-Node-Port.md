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
节点进程异常停止后，可通过以下命令修复状态并启动
``` 
./lambda start --p2p.laddr tcp://0.0.0.0:26656 --rpc.laddr tcp://0.0.0.0:26657 --daemonize --log.file /tmp/lambda.log --replay-last-block
```


