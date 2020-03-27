# Storage0.2.4升级

* [下载安装包并解压](#下载安装包并解压)
* [minernode升级](#minernode升级)
* [storagenode升级](#storagenode升级)
* [storagecli升级](#storagecli升级)

新矿工和存储节点接入参考：[配置矿工和存储节点](Testnet-Miner-Guide.md)

## 下载安装包并解压
创建目录并进入 
```
mkdir -p ~/LambdaIM && cd ~/LambdaIM
```
下载安装包
```
wget https://github.com/LambdaIM/launch/releases/download/Storage0.2.4/lambda-storage-0.2.4-testnet.tar.gz

如下载缓慢可使用下面的链接：
wget http://download.lambdastorage.com/lambda-storage/0.2.4/lambda-storage-0.2.4-testnet.tar.gz
```
解压安装包
```
tar zxvf lambda-storage-0.2.4-testnet.tar.gz
```
进入解压后的目录
```
cd lambda-storage-0.2.4-testnet
```

## minernode升级
### minernode升级
``` 
./minernode upgrade
```

### 重启minernode
[log_file_path] 指定矿工日志完整路径

1.停止minernode：
```
./minernode run --stop
```
如停止失败，使用以下命令停掉minernode：
```
kill `ps aux | grep 'minernode' |grep -v grep| awk '{print $2}'`
```
2.启动minernode：
```
./minernode run --query-interval 5 --daemonize --log.file [log_file_path]
```

如[your-account-name]_miner_key.json没有移动到~/.lambda_miner/config/default_miner_key.json，则加上--key-file参数启动：
```
./minernode run --query-interval 5 --daemonize --log.file [log_file_path] --key-file [filepath/your-account-name]_miner_key.json
```

## storagenode升级
### 备份旧版配置文件
``` 
cp ~/.lambda_storage/config/config.toml ~/LambdaIM/lambda-storage-0.2.4-testnet/
```
### storagenode升级
``` 
./storagenode upgrade
```

### 修改配置和移动目录
修改新版配置`~/.lambda_storage/config/config.toml`下的`storage.data_dir`，将旧版配置的存储目录`storage.data_dir`和挖矿目录`mining.mining_dir`放到storage.data_dir目录下

注意：如旧版的存储目录、挖矿目录 和 新版的storage.data_dir均为默认值，可跳过此步

``` 
以如下旧版配置为例
[storage]
# 存储目录
data_dir = ["/data/test1/store1"]
[mining]
# 挖矿目录
mining_dir = ["/data/test1/mining1"]

新版需修改配置如下
vi ~/.lambda_storage/config/config.toml
[storage]
data_dir = ["/data/test1"]

移动存储和挖矿目录
mv /data/test1/store1 /data/test1/store
mv /data/test1/mining1 /data/test1/mining
```

### 重建索引
``` 
./storagenode info index --rebuild
```

### 重启storagenode
[log_file_path] 指定storagenode运行日志路径

1.停止storagenode：
```
./storagenode run --stop
```
如停止失败，使用以下命令停掉storagenode：
```
kill `ps aux | grep 'storagenode' |grep -v grep| awk '{print $2}'`
```

2.启动storagenode：
```
./storagenode run --daemonize --log.file [log_file_path]
```

## storagecli升级
### 清除历史token
``` 
./storagecli token clear
```

### 同步订单token  
[account-name] 为发起买单账户名称
```
./storagecli token sync [account-name]
```


