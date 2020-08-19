# storage0.2.7.3升级

* [下载安装包并解压](#下载安装包并解压)
* [停止minernode和storagenode](#停止minernode和storagenode)
* [minernode升级配置文件](#minernode升级配置文件)
* [storagenode升级配置文件](#storagenode升级配置文件)
* [minernode重启](#minernode重启)
* [storagenode重启](#storagenode重启)

新矿工和存储节点接入参考：[配置矿工和存储节点](Mainnet-Miner-Guide.md)  

以下为旧版本升级 升级到 `0.2.7.3` 步骤  


### 下载安装包并解压

创建目录并进入 

```
mkdir -p ~/LambdaIM && cd ~/LambdaIM
```
下载安装包
```
http://download.lambdastorage.com/lambda-storage/0.2.7.3/lambda-storage-0.2.7.3.tar.gz
```
解压安装包
```
tar zxvf lambda-storage-0.2.7.3.tar.gz
```
进入解压后的目录
```
cd lambda-storage-0.2.7.3
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

### （可选）修改矿工和存储metadb路径
#### 修改矿工metadb路径
默认路径为`/root/.lambda_miner`，以修改为`/data1/test`为例

1. 移动`/root/.lambda_miner`下的`var`、`kademlia`到`/data1/test/`:
```
mv /root/.lambda_miner/{var,kademlia} /data1/test/
```
2. 修改配置：
```
./minernode config db.meta_dir /data1/test
```
        
#### 修改存储metadb路径
默认路径为`/root/.lambda_storage/meta`，以修改为`/data1/test/meta`为例）

1. 移动`/root/.lambda_storage`下的`meta`到`/data1/test/`:
```
mv /root/.lambda_storage/meta /data1/test/
```
2. 修改配置：
```
./storagenode config storage.meta_dir /data1/test/meta
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
