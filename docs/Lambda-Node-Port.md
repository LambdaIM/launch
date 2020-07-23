# Lambda端口说明

### 节点端口
26656 p2p通讯端口  
26657 tendermint默认的rpc接口端口  
13659 lambda的rpc端口，主要是查询相关业务  

### 矿工端口 
13000 矿工服务端口
14000 存储服务端口

### 矿工切换验证节点
如果当前链接的验证节点慢，可切换自己的验证节点
```
./lambdacli config node tcp://[nodeip]:26657
```  
        
- `[nodeip]` 需要更换的验证节点`公网IP`

