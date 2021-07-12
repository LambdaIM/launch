# 主网同步节点 接入教程

### 1. 下载安装包并解压
`创建目录并进入`
```
mkdir -p ~/LambdaIM && cd ~/LambdaIM
```
`下载安装包`
```
wget https://github.com/LambdaIM/launch/releases/download/v0.3.4/lambda-0.3.4-release.tar.gz

如下载缓慢可使用下面的链接：
wget http://download.lambdastorage.com/lambda/0.3.4/lambda-0.3.4-release.tar.gz
```

`解压安装包`
```
tar zxvf lambda-0.3.4-release.tar.gz && cd lambda-0.3.4-release
```

### 2. 初始化节点  
`将下面命令中的[your-moniker]替换成您自定义的节点名称，不用加中括号`  
`注意：这里的 your-moniker 必须使用英文，用于P2P网络`
```
./lambda init [your-moniker] --chain-id lambda-chain-3.0
```
如果初始化报错，可能是由于有老版本的配置数据导致，可以通过下面的命令清除错误数据
```
rm ~/.lambda/config/config.toml ~/.lambda/config/genesis.json
./lambda unsafe-reset-all
```

**注意**

不要删除~/.lambda/config下的`priv_validator_key.json`和`node_key.json`文件，
如果丢失会导致节点无法再正常加入共识网络，请节点注意备份

### 3. 覆盖genesis.json文件
```
\cp -rf ./genesis.json ~/.lambda/config/genesis.json
```

### 4. 配置种子节点  
编辑`~/.lambda/config/config.toml`文件，将文件中的seeds字段的值替换如下
```
vim ~/.lambda/config/config.toml
seeds = "72e1dd22f2c3effc4e6ff842035f109480a997ae@seednodes1.oneweb.one:26656"

如需配置多个节点需以逗号隔开，例如：
seeds = "72e1dd22f2c3effc4e6ff842035f109480a997ae@seednodes1.oneweb.one:26656,d3440b0b7a0ccf419f506a1242431813cf8a699c@39.104.97.255:26656,98a0a749080b367d218f68b628b2db3d8d175af9@39.100.6.247:26656,91fa14e2c8da164ff7969f2bbc0ba5c6e206da8a@101.201.65.116:26656"
```


主网目前种子节点列表：
```
国外种子节点
dd3360f3a4334432af394a835662a2b21bf406e2@seednodes.oneweb.one:26656

国内种子节点列表
72e1dd22f2c3effc4e6ff842035f109480a997ae@seednodes1.oneweb.one:26656
d3440b0b7a0ccf419f506a1242431813cf8a699c@39.104.97.255:26656
98a0a749080b367d218f68b628b2db3d8d175af9@39.100.6.247:26656
91fa14e2c8da164ff7969f2bbc0ba5c6e206da8a@101.201.65.116:26656 
```


**注意**

当前支持配置多个种子节点，通过`,`隔开  
切换节点后需要kill掉节点服务并且重启

### 5. 启动节点  
```
nohup ./lambda start --p2p.laddr tcp://0.0.0.0:26656 --rpc.laddr tcp://0.0.0.0:26657 >> lambda.log 2>&1 &
```
