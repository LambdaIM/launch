# storage0.2.4升级

* [下载安装包并解压](#下载安装包并解压)
* [停止minernode和storagenode](#停止minernode和storagenode)
* [minernode升级配置文件](#minernode升级配置文件)
* [storagenode升级配置文件](#storagenode升级配置文件)
* [minernode重启](#minernode重启)
* [storagenode重启](#storagenode重启)

新矿工和存储节点接入参考：[配置矿工和存储节点](Testnet-Miner-Guide.md)  

以下为 旧版0.2.4 升级到 lambda-storage-0.2.5-testnet 步骤（不支持旧版 0.2.3 直接升级到此版本）

0.2.3升级到0.2.4参考：[Storage0.2.4升级](Testnet-Storage-Upgrade023.md)



### 下载安装包并解压

创建目录并进入 

```
mkdir -p ~/LambdaIM && cd ~/LambdaIM
```
下载安装包
```
wget https://github.com/LambdaIM/launch/releases/download/v0.5.3/lambda-storage-0.3.0-rc1-testnet.tar.gz
```
解压安装包
```
tar zxvf lambda-storage-0.3.0-rc1-testnet.tar.gz
```
进入解压后的目录
```
cd lambda-storage-0.3.0-rc1-testnet
```

### 停止minernode和storagenode
1.停止minernode：
```
./minernode run --stop
```
返回结果如下即停止成功：
```
stop daemon process from minernode.pid:22937 successfully
```
如果返回结果停止失败，使用以下命令停掉minernode：
```
kill `ps aux | grep 'minernode' |grep -v grep| awk '{print $2}'`
```

2.停止storagenode：
```
./storagenode run --stop
```
返回结果如下即停止成功：
```
stop daemon process from storagenode.pid:22937 successfully
```
如果返回结果停止失败，使用以下命令停掉storagenode：
```
kill `ps aux | grep 'storagenode' |grep -v grep| awk '{print $2}'`
```

### minernode升级

```
./minernode upgrade
```

### storagenode升级

```
./storagenode upgrade
```

### 重启minernode
1.修改lambdacli配置
```
./lambdacli config chain-id lambda-chain-test5.3
```

2.启动minernode：  
[log_file_path] 指定矿工日志完整路径
```
./minernode run --query-interval 5 --daemonize --log.file [log_file_path]
```

如`[your-account-name]_miner_key.json`没有移动到`~/.lambda_miner/config/default_miner_key.json`，则加上`--key-file`参数启动：
```
./minernode run --query-interval 5 --daemonize --log.file [log_file_path] --key-file [filepath/your-account-name]_miner_key.json
```

### 重启storagenode
启动storagenode：
[log_file_path] 指定storagenode运行日志路径
```
./storagenode run --daemonize --log.file [log_file_path]
```
