# 矿工和存储节点迁移

注意：矿工或存储节点迁移机器后如IP有变化，可能会有一段时间连不上存储网络

## 矿工迁移
### 默认矿工目录[重要]  
配置目录[**重要、进行备份**]  
`~/.lambdacli`  
`~/.lambda_miner`  

如矿工子账户json文件未移动到`~/.lambda_miner/config/default_miner_key.json`，也需要进行备份

### 迁移机器
1. 下载存储程序安装包
2. 将旧机器`~/.lambdacli`和`~/.lambda_miner`目录、矿工子账户json文件 覆盖至新机器`~/.lambdacli`和`~/.lambda_miner`
3. 如公网IP有变化，需要将`~/.lambda_miner/config/config.toml`中 旧机器IP地址 修改为 新机器的IP地址，  
   另外连接该矿工的存储节点配置`~/.lambda_storage/config/config.toml`中`storage.miner_address` 矿工服务IP也需要对应修改，并重启存储节点服务
4. 停掉旧机器的minernode程序，启动新机器的minernode程序

## 存储节点迁移
注意：不要修改存储节点名称

### 默认存储目录[重要]
配置目录[**重要、进行备份**]  
`~/.lambda_storage`  

如存储节点配置`~/.lambda_storage/config/config.toml`中数据存储目录`storage.data_dir`不是默认值，需要备份对应目录

### 迁移机器
1. 下载存储程序安装包
2. 停掉旧机器的storagenode程序
3. 将旧机器`~/.lambda_storage`和 `数据存储目录` 覆盖至新机器
4. 如果新机器数据存储目录有变化，需要对应修改`~/.lambda_storage/config/config.toml`中的`storage.data_dir`
5. 将`~/.lambda_storage/config/config.toml`中 旧机器IP地址 修改为 新机器IP
6. 启动新机器的storagenode程序

### 迁移数据
将存储数据从盘A迁移到盘B

1. 停止storagenode程序
2. 将 旧盘存储数据 移动至新盘目录
3. 修改`~/.lambda_storage/config/config.toml`中的`storage.data_dir`
4. 重新启动storagenode程序

举个例子：
``` 
假如旧盘存储数据路径为：~/.lambda_storage,/data1/test
新盘路径为：/data3/test,/data4/test 

移动存储和挖矿目录
mkdir -p /data3/test/
mv ~/.lambda_storage/store /data3/test/
mv ~/.lambda_storage/mining /data3/test/
mv /data1/test /data4/test

修改存储数据目录配置
./storagenode config storage.data_dir /data3/test,/data4/test
```
