# 测试网Validator 0.4.8 升级教程

新节点接入参考[测试网节点0.4.8 接入教程](Testnet-Validator-Guide.md)

测试网节点从0.4.7版本升级到0.4.8版本参考如下步骤

### 1. 下载安装包并解压
`创建目录并进入`
```
mkdir -p ~/LambdaIM && cd ~/LambdaIM  
```
如已有~/LambdaIM目录则直接进入目录：`cd ~/LambdaIM` 

`下载安装包`
```
wget https://github.com/LambdaIM/launch/releases/download/v0.4.8/lambda-0.4.8-testnet.tar.gz

如下载缓慢可使用下面的链接：
wget http://download.lambdastorage.com/lambda/0.4.8/lambda-0.4.8-testnet.tar.gz
```

`解压安装包`
```
tar zxvf lambda-0.4.8-testnet.tar.gz && cd lambda-0.4.8-testnet
```
### 2. 停止节点服务

```
./lambda stop

返回如下结果即为停止成功：
stop daemon process from lambda.pid:28638 successfully

如停止失败，可使用以下命令停止进程：
kill `ps aux | grep lambda |grep -v grep| awk '{print $2}'`
```
**注意**：  
1. 成功停止节点服务后，禁止使用v0.4.7版本的lambda程序做任何操作。  
2. 保证后续执行的lambda、lambdacli程序均为v0.4.8版本。  

### 3. 覆盖genesis.json文件
```
\cp -rf ./genesis.json ~/.lambda/config/genesis.json
```

### 4. 修改lambdacli配置
要确保机器已开启端口26656, 26657
```
./lambdacli config chain-id lambda-chain-test4.8
```

### 5. 备份和恢复db
#### 备份db
备份db到`~/LambdaIM/lambda_bak`目录
```
mkdir -p ~/LambdaIM/lambda_bak
mv ~/.lambda/data/pdp*.db ~/LambdaIM/lambda_bak/
mv ~/.lambda/data/market*.db ~/LambdaIM/lambda_bak/
```
#### 清除历史数据
```
./lambda unsafe-reset-all
```
#### 恢复db
```
cp -r ~/LambdaIM/lambda_bak/*.db ~/.lambda/data/
```

### 6. 启动节点  
```
./lambda start --p2p.laddr tcp://0.0.0.0:26656 --rpc.laddr tcp://0.0.0.0:26657 --daemonize --log.file /tmp/lambda.log
```

### 7. 启动rest-server服务
rest-server服务可提供给钱包和storagecli连接
```
nohup ./lambdacli rest-server --node tcp://0.0.0.0:26657 --laddr tcp://0.0.0.0:13659 >> /tmp/lambdacli.log 2>&1 &
```

**查看/tmp/lambda.log日志正常，即节点升级成功。不需要再执行后面的操作。**

==============

### 升级注意事项
**如升级失败**，可使用社区提供的区块链数据包启动节点

**注意：进行以下操作前，保证上面前4步执行完成。**

#### 清除历史数据
```
./lambda unsafe-reset-all
```

#### 使用社区提供的区块链数据包启动节点
下载数据压缩包lambda_0.4.8_data.tar.gz
``` 
wget http://download.lambdastorage.com/lambda/0.4.8/lambda_0.4.8_data.tar.gz
```
解压`lambda_0.4.8_data.tar.gz`到`~/.lambda/`目录下（解压过程耗时较长，请耐心等待）
``` 
tar -zxvf lambda_0.4.8_data.tar.gz -C ~/.lambda/
```
启动节点
```
./lambda start --p2p.laddr tcp://0.0.0.0:26656 --rpc.laddr tcp://0.0.0.0:26657 --daemonize --log.file /tmp/lambda.log
```
