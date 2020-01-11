# storage0.2.2升级

* [下载安装包并解压](#下载安装包并解压)
* [minernode升级配置文件](#minernode升级配置文件)
* [minernode升级配置文件](#minernode升级配置文件)
* [minernode重启](#minernode重启)
* [storagenode重启](#storagenode重启)

以下为lambda-storage-0.2.1-testnet 升级到 lambda-storage-0.2.2-testnet 步骤

### 下载安装包并解压

创建目录并进入 

```
mkdir -p ~/LambdaIM && cd ~/LambdaIM
```
下载安装包
```
wget https://github.com/LambdaIM/launch/releases/download/Storage0.2.2/lambda-storage-0.2.2-testnet.tar.gz
```
解压安装包
```
tar zxvf lambda-storage-0.2.2-testnet.tar.gz
```
进入解压后的目录
```
cd lambda-storage-0.2.2-testnet
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
[log_file_path] 指定矿工日志完整路径

1. 停止minernode：
```
./minernode run --stop
```
返回结果如下即停止成功：
```
stop daemon process from minernode.pid:22937 successfully
```
如果返回结果停止失败，使用以下命令停掉minernode：
```
kill -9 `ps aux | grep 'minernode' |grep -v grep| awk '{print $2}'`
```
2. 启动minernode：
```
./minernode run --query-interval 5 --daemonize --log.file [log_file_path]
```

如[your-account-name]_miner_key.json没有移动到~/.lambda_miner/config/default_miner_key.json，则加上--key-file参数启动：
```
./minernode run --query-interval 5 --daemonize --log.file [log_file_path] --key-file [filepath/your-account-name]_miner_key.json
```

### 重启storagenode
[log_file_path] 指定storagenode运行日志路径

1. 停止storagenode：
```
./storagenode run --stop
```
返回结果如下即停止成功：
```
stop daemon process from storagenode.pid:22937 successfully
```
如果返回结果停止失败，使用以下命令停掉storagenode：
```
kill -9 `ps aux | grep 'storagenode' |grep -v grep| awk '{print $2}'`
```

2. 启动storagenode：
```
./storagenode run --daemonize --log.file [log_file_path]
```
