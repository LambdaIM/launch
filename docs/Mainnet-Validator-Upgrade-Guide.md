# 主网Validator 0.5.3 升级教程

主网新节点接入可参考：[主网Validator接入教程](Mainnet-Validator-Guide.md)  

### 1. 下载安装包并解压
`创建目录并进入`
```
mkdir -p ~/LambdaIM && cd ~/LambdaIM  
```
如已有~/LambdaIM目录则直接进入目录：`cd ~/LambdaIM` 

`下载安装包`
```
wget https://github.com/LambdaIM/launch/releases/download/v0.5.3/lambda-0.5.3-release.tar.gz

如下载缓慢可使用下面的链接：
wget http://download.lambdastorage.com/lambda/0.5.3/lambda-0.5.3-release.tar.gz
```

`解压安装包`
```
tar zxvf lambda-0.5.3-release.tar.gz && cd lambda-0.5.3-release
```
### 2. 停止节点服务
#### 停止节点服务
``` 
./lambda stop
```
返回如下结果即为停止成功：
```
stop daemon process from lambda.pid:28638 successfully
```

#### 停止rest-server服务
```
kill `ps aux | grep 'lambdacli rest-server' |grep -v grep| awk '{print $2}'`
```

### 3. 启动节点  
```
./lambda start --p2p.laddr tcp://0.0.0.0:26656 --rpc.laddr tcp://0.0.0.0:26657 --daemonize --log.file /tmp/lambda.log
```

### 4. 启动rest-server服务
rest-server服务可提供给钱包、矿工和storagecli连接
```
nohup ./lambdacli rest-server --node tcp://0.0.0.0:26657 --laddr tcp://0.0.0.0:13659 >> /tmp/lambdacli.log 2>&1 &
```

### 5. 查看节点运行状态
```
./lambda status
```
返回结果如下即运行正常：
``` 
lambda.pid is running, pid is 5993
```



