

相关资源

矿工管理程序下载地址：[https://github.com/LambdaIM/launch/releases/tag/StorageManager0.1.11](https://github.com/LambdaIM/launch/releases/tag/StorageManager0.1.11)

钱包下载地址：[https://github.com/LambdaIM/launch/releases/tag/Wallet0.4.39](https://github.com/LambdaIM/launch/releases/tag/Wallet0.4.39)

挖矿程序安装包：[https://github.com/LambdaIM/launch/releases/tag/Storage0.2.1](https://github.com/LambdaIM/launch/releases/tag/Storage0.2.1)


使用矿工管理程序配合钱包即可添加配置矿工服务及存储节点服务，非常便利


点击 StorageManager 打开管理程序

![图片](https://uploader.shimo.im/f/UsdCXWQKTmkqiCI5.png!thumbnail)

这是管理程序的首页

![图片](https://uploader.shimo.im/f/P3Cj4MiVOSIBB99I.png!thumbnail)

# 1 添加矿工节点服务器
点击 添加节点 ，选择通过密码添加节点或通过私钥添加节点

![图片](https://uploader.shimo.im/f/Ik5ATX9eNvgWWGLd.png!thumbnail)

1 通过用户名和密码添加 

![图片](https://uploader.shimo.im/f/KO24v3FdJncpJPMW.png!thumbnail)

2 通过私钥添加

![图片](https://uploader.shimo.im/f/bYRHXEV3d3EyhUif.png!thumbnail)

添加成功后可以看到相关操作

![图片](https://uploader.shimo.im/f/CJ4oW9spwJQ0gCML.png!thumbnail)

# 2钱包质押
![avatar](img/valist@2x.png)
点击到验证节点 列表
![avatar](img/valist2@2x.png)
点击查看验证节点详细信息
![avatar](img/vainfo@2x.png)
点击质押按钮进行质押，质押不得少于1TBB
![avatar](img/zhiyainfo@2x.png)


# 3钱包创建挖矿子账户及导出

在钱包首页点击子账户链接，切换到子账户标签页

![avatar](img/sonaccount.png)

可以看到创建矿工子账户和导入按钮

## 创建子账户
点击创建子账户按钮，打开创建子账户弹窗

![avatar](img/sonaccountd1.png)

创建矿工子账户需要输入当前钱包的助记词和密码，输入备注方便记忆

也可以导入钱包或区块链程序导出的子账户

## 导入子账户
如果已有子账户json文件，可通过钱包导入子账户。如已进行上面创建子账户操作，可跳过此步。

点击导入按钮，打开导入子账户弹窗

![avatar](img/sonaccountd2.png)

导入子账户需要选择子账户的json文件和当前钱包的密码

## 导出子账户
如果需要在矿工管理程序或区块链程序中使用挖矿子账户，可以导出子账户

![avatar](img/sonaccountd3.png)

导出子账户需要输入当前钱包的密码

例如 在矿工管理程序中选择钱包导出的子账户
![avatar](img/sonaccountd5.png)

# 4矿工初始化
点击初始化按钮打开初始化界面

![图片](https://uploader.shimo.im/f/RnAchczcOTAGlqp5.png!thumbnail)

初始化需要填写的信息注意事项

1. 验证节点IP：链接测试网就填写测试网的验证节点IP，链接主网就填写主网的节点IP

2. 端口：填写对应验证节点的rpc端口，一般为26657

3. 挖矿子账户有选择本地文件和选择本地钱包导出的挖矿子账户两种方式

  选择本地文件是 本地有之前通过钱包或链导出的挖矿子账户的json文件

  如果本机也安装了lamb钱包，钱包导出的挖矿子账户就会出现在下拉列表中

4. 安装文件包，需要先将需要安装的挖矿程序包下载到管理程序指定的文件夹中，点击提交的时候会自动安装包上传。

![图片](https://uploader.shimo.im/f/ISFyCtr10PoFvz4M.png!thumbnail)

# 5钱包初始化矿工

点击钱包的市场页面，再点击我出售的空间面板，可以看到矿工初始化按钮

![avatar](img/marketd1.png)

点击矿工初始化按钮，打开创建矿工弹窗

![avatar](img/marketd2.png)

创建矿工需要选择钱包中的子账户和部署矿工服务器的dhtid
可以在 矿工管理程序中获取一个矿工服务的 dhtid
例如

![avatar](img/marketd3.png)

# 6配置矿工节点
点击配置节点按钮打开配置界面

![图片](https://uploader.shimo.im/f/30euDM6ET8gEMMH2.png!thumbnail)

矿工节点配置分5个模块 分别是api_key,db,kad,log,server

启动矿工必须要填写的是配置为

server.address

server.private_address

kad.external_address

kad.bootstrap_addr

api_key.root_secret_seed

参考如下说明进行配置(实际修改配置文件为~/.lambda_miner/config/config.toml):

```
# 服务需要监听的地址
# 以本机内网IP为 192.168.10.10，端口映射的外网IP为 200.200.200.100 为例
[server]
# 对外提供服务的地址，推荐配置为内网地址做端口映射到外网IP
address = "192.168.10.10:13000"
# 对内提供服务的地址，主要是给StorageNode使用，推荐配置为内网地址
private_address = "192.168.10.10:13001"
debug_log_traffic = "false"

[kad]
# DHT接入节点地址，存储网络提供，可填写多个，以 47.94.129.97:13000 为例
# 可选dht地址：39.105.148.217:13000/47.94.129.97:13000/47.93.196.236:13000/182.92.66.63:13000
bootstrap_addr = ["47.94.129.97:13000"]
# time you would wait to connect dht seed node
bootstrap_backoff_max = "30s"
bootstrap_backoff_base = "1s"
db_path = "/root/.lambda_miner/kademlia"
# this should listen at Public IP
## 对外暴露的提供服务的地址
external_address = "200.200.200.100:13000"
alpha = 3

[kad.routing_table_config]
bucket_size = 20
replacement_cache_size = 5

[api_key]
#root access key，不能为空
root_secret_seed = "yah"

[log]
level = "info"
output_file = "stdout"

[db]
# db config
lru_cache = "131072"
keep_log_file_num = "100"
write_buffer_size = "134217728"
recycle_log_file_num = "0"
target_file_size_base = "268435456"
max_write_buffer_number = "4"
max_bytes_for_level_base = "4294967296"
level_0_stop_writes_trigger = "24"
target_file_size_multiplier = "1"
max_background_compactions = "2"
max_bytes_for_level_multiplier = "2"
level_0_slowdown_writes_trigger = "17"
level_0_file_num_compaction_trigger = "8"
level_compaction_dynamic_level_bytes = "0"
compaction_algorithm = "0"
rate_bytes_per_sec = "10240"
data_backup_path = ""
data_backup_interval = "300000000000"
```
配置完成后可以点击启动按钮，启动矿工服务，成功后状态会变成绿色的☑️

![图片](https://uploader.shimo.im/f/zmffho7Ly40IQhyE.png!thumbnail)

如果启动后状态没有变化 可以点击打开远程日志按钮，查看日志

一般如果是缺少配置导致的失败，日志里面会列出比填写的配置项是哪些

![图片](https://uploader.shimo.im/f/94q81R6xm0cshGqr.png!thumbnail)

# 7添加存储节点
点击服务器名称进入矿工详情页面

![图片](https://uploader.shimo.im/f/cDkJUYFdL8cpXPfD.png!thumbnail)

添加存储节点服务器的方式和添加矿工的方式类似

添加完成后进入点击配置存储节点

# 8配置存储节点
![图片](https://uploader.shimo.im/f/FxTCo22Hr2MVimU8.png!thumbnail)

存储节点必填的配置

server.address

server.private_address

kad.bootstrap_addr

kad.external_address

storage.storage_name

storage.miner_address

storage.root_secret_seed

`~/.lambda_storage/config/config.toml` 配置说明

```
# 服务需要监听的地址
# 以本机内网IP为 192.168.10.20，端口映射的外网IP为 200.200.200.200 为例
[server]
# 对外提供服务的地址，推荐配置为内网地址做端口映射到外网IP
address = "192.168.10.20:14000"
# 对内提供服务的地址，主要是给StorageNode使用，推荐配置为内网地址
private_address = "192.168.10.20:14001"
debug_log_traffic = "false"


[kad]
# address you want kad to connect with
# DHT接入节点地址，可以是存储网络提供的地址，也可以是minernode暴露到外网的IP，这里以 47.94.129.97:13000 为例
# 可选dht地址：39.105.148.217:13000/47.94.129.97:13000/47.93.196.236:13000/182.92.66.63:13000
bootstrap_addr = ["47.94.129.97:13000"]
# time you would wait to connect dht seed node
bootstrap_backoff_max = "30s"
bootstrap_backoff_base = "1s"
db_path = "/root/.lambda_storage/kademlia"
# this should listen at Public IP
external_address = "200.200.200.200:14000"
alpha = 3

[kad.routing_table_config]
bucket_size = 20
replacement_cache_size = 5

[log]
level = "info"
output_file = "stdout"

[storage]
## 用于生成apikey的种子内容，不能为空
root_secret_seed = "fasdf"
## 存储路径，可填写多个以逗号隔开
data_dir = [ "/root/.lambda_storage/store"]
## minernode对内提供服务的地址，即它的server.private_address
miner_address = "192.168.10.10:13001"
## 存储节点的名字，需要在矿池内部唯一，即连接同一矿工的多个storagenode的storage_name不能重复
storage_name = "machine1"

[mining]
## 挖矿记录的数据文件
db_path = "/root/.lambda_storage/statementdb"
## 存储挖矿文件(删除的)的存储路径，可填写多个以逗号隔开
mining_dir = [ "/root/.lambda_storage/mining"]
```
配置完成之后

选择存储节点，然后点击启动

![图片](https://uploader.shimo.im/f/vPR3VcvxbrYnGP3k.png!thumbnail)

如果启动后状态没有变化 可以点击打开远程日志按钮，查看日志

一般如果是缺少配置导致的失败，日志里面会列出比填写的配置项是哪些

![图片](https://uploader.shimo.im/f/ZhdUEQERXdMIAGWk.png!thumbnail)

# 6获取DHT ID
在钱包中创建矿工时候需要填写矿工dhtid

在矿工详情页面即可获取到dhtid

![图片](https://uploader.shimo.im/f/faYIvLug3yg1seUw.png!thumbnail)

