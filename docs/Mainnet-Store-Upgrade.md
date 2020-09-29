# storage0.2.8升级

* [下载安装包并解压](#下载安装包并解压)
* [停止minernode和storagenode](#停止minernode和storagenode)
* [minernode升级](#minernode升级)
* [storagenode升级](#storagenode升级)
* [minernode重启](#minernode重启)
* [storagenode重启](#storagenode重启)

新矿工和存储节点接入参考：[配置矿工和存储节点](Mainnet-Miner-Guide.md)  

以下为旧版本升级 升级到 `0.2.8` 步骤  


### 下载安装包并解压

创建目录并进入 

```
mkdir -p ~/LambdaIM && cd ~/LambdaIM
```
下载安装包
```
http://download.lambdastorage.com/lambda-storage/0.2.8/lambda-storage-0.2.8.tar.gz
```
解压安装包
```
tar zxvf lambda-storage-0.2.8.tar.gz
```
进入解压后的目录
```
cd lambda-storage-0.2.8
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
启动`minernode`：  
[log_file_path] 指定矿工日志完整路径
```
./minernode run --query-interval 5 --daemonize --log.file [log_file_path]
```

如`[your-account-name]_miner_key.json`没有移动到`~/.lambda_miner/config/default_miner_key.json`，则加上`--key-fil`e参数启动：
```
./minernode run --query-interval 5 --daemonize --log.file [log_file_path] --key-file [filepath/your-account-name]_miner_key.json
```

### 重启storagenode
启动`storagenode`：
[log_file_path] 指定`storagenode`运行日志路径
```
./storagenode run --daemonize --log.file [log_file_path]
```
