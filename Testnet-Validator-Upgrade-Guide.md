# 测试网Validator 0.4.7 升级教程

新节点接入参考[测试网节点0.4.7 接入教程](Testnet-Validator-Guide.md)

测试网节点从0.4.6版本升级到0.4.7版本参考如下步骤

### 1. 下载安装包并解压
`创建目录并进入`
```
mkdir -p ~/LambdaIM && cd ~/LambdaIM  
```
如已有~/LambdaIM目录则直接进入目录：`cd ~/LambdaIM` 

`下载安装包`
```
wget https://github.com/LambdaIM/launch/releases/download/v0.4.7/lambda-0.4.7-testnet.tar.gz

如下载缓慢可使用下面的链接：
wget http://download.lambdastorage.com/lambda/0.4.7/lambda-0.4.7-testnet.tar.gz
```

`解压安装包`
```
tar zxvf lambda-0.4.7-testnet.tar.gz && cd lambda-0.4.7-testnet
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
1. 成功停止节点服务后，禁止使用v0.4.6版本的lambda程序做任何操作。  
2. 保证后续执行的lambda、lambdacli程序均为v0.4.7版本。  

### 3. 执行升级脚本
说明：
1. 该升级脚本用于将0.4.6版本`/root/.lambda/config/lambda.toml` 中  [db]下的几项配置对应目录 移动到`/root/.lambda/config/config.toml` 配置的 `db_dir` 目录下。
2. `lambda init`和`lambda start`未指定`--home`参数时，使用的默认lambda home为`~/.lambda`；默认`db_dir = "data"`；即默认home和默认配置下 实际lambda相关db会存放在`~/.lambda/data`

[lambda_home_dir] 脚本支持输入指定路径作为 lambda home 路径，若不加上该参数，默认读取 ~/.lambda 目录
``` 
./upgrade_db.sh [lambda_home_dir]
```
lambda home为默认值时执行 `./upgrade_db.sh` 即可

以下提示[Y/n]时需要手动输入y，输出结果如下：
```
Move /root/.lambda/data/application.db to /root/.lambda/data? [Y/n] y
mv: "/root/.lambda/data/application.db" 与"/root/.lambda/data/application.db" 为同一文件
Move /root/.lambda/market.db to /root/.lambda/data? [Y/n] y
"/root/.lambda/market.db" -> "/root/.lambda/data/market.db"
Move /root/.lambda/pdp.db to /root/.lambda/data? [Y/n] y
"/root/.lambda/pdp.db" -> "/root/.lambda/data/pdp.db"
Move /root/.lambda/pdp.ms.db to /root/.lambda/data? [Y/n] y
"/root/.lambda/pdp.ms.db" -> "/root/.lambda/data/pdp.ms.db"
Move /root/.lambda/identity to /root/.lambda? [Y/n] y
mv: "/root/.lambda/identity" 与"/root/.lambda/identity" 为同一文件
```

执行完脚本之后，确认 `lambda.toml`  配置目录中的各个db都成功移动到了 db_dir配置项下。
``` 
ls -l ~/.lambda/data

总用量 44K
drwxr-xr-x 2 root root 4.0K 3月  24 09:06 application.db
drwxr-xr-x 2 root root 4.0K 3月  24 08:16 blockstore.db
drwx------ 2 root root 4.0K 3月  24 08:10 cs.wal
drwxr-xr-x 2 root root 4.0K 3月  24 02:19 evidence.db
drwxr-xr-x 2 root root 4.0K 3月  24 07:41 market.db
drwxr-xr-x 2 root root 4.0K 3月  24 02:19 market.ms.db
drwxr-xr-x 2 root root 4.0K 3月  24 08:58 pdp.db
drwxr-xr-x 2 root root 4.0K 3月  24 02:19 pdp.ms.db
-rw------- 1 root root  401 3月  27 16:29 priv_validator_state.json
drwxr-xr-x 2 root root 4.0K 3月  24 07:32 state.db
drwxr-xr-x 2 root root 4.0K 3月  24 02:19 tx_index.db
```

如执行脚本过程中遇到文件路径不对的或迁移失败的db，也可以手动迁移，只需要分别将`application.db`、 `market.db`、`pdp.db`、`pdp.ms.db`、 `identity` 目录移动到 `/root/.lambda/config/config.toml` 配置的 `db_dir` 目录下。  

命令：`mv [源文件] [新目录]`  
例如：
``` 
源文件为/root/.lambda/data/application.db
config.toml中设置db_dir = "/lambda/test/data"（即移动到新目录/lambda/test/data下）
mv /root/.lambda/data/application.db /lambda/test/data/
```

### 4. 版本检查和自动回滚
``` 
./lambda state fix
```

### 5. 启动节点  
```
./lambda start --p2p.laddr tcp://0.0.0.0:26656 --rpc.laddr tcp://0.0.0.0:26657 --daemonize --log.file /tmp/lambda.log
```

### 6. 启动rest-server服务
rest-server服务可提供给钱包和storagecli连接
```
nohup ./lambdacli rest-server --node tcp://0.0.0.0:26657 --laddr tcp://0.0.0.0:13659 >> /tmp/lambdacli.log 2>&1 &
```
