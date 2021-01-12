# 默认存储目录[重要]
数据目录

`~/.lambda/data`

配置目录[**重要、进行备份**]

`~/.lambda/config`

# 迁移机器
1. 下载lambda程序
2. 运行 `./lambda init [name]`
3. 将旧机器`~/.lambda/config`目录覆盖至新机器`~/.lambda/config`
4. （二选一）停掉旧机器的lambda程序，启动新机器的lambda程序，重新同步区块  
（二选一）停掉旧机器的lambda程序，[使用社区提供的区块链数据包启动节点](http://docs.lambda.im/Mainnet-Validator-Guide/#_2)(目前主网区块较多，建议用此方式进行同步更快速)  
（**注意：一定要先停掉旧机器lambda服务，以免出现双签情况**）
5. 如果节点被惩罚，参考重新加入共识网络

# 迁移数据
将数据从盘A迁移到盘B

1. 将`~/.lambda/data` 移动至新盘目录
2. 创建`~/.lambda/data`至 新盘目录的软链接，命令：`ln -s  [新盘目录]  ~/.lambda/data`
3. 检查软连接是否创建成功，命令：`ls -al ~/.lambda/data`
4. 重新启动lambda程序
5. 如果节点被惩罚，参考重新加入共识网络

软链接相当于原目录的快捷方式，可以直接从原位置访问新目录的位置，

举个例子：
``` 
假如新盘路径为：/var/lambda/data 

ln -s  /var/lambda/data ~/.lambda/data

lrwxr-xr-x   1 root  staff    16B  3  6 14:43 data -> /var/lambda/data

访问~/.lambda/data的目录会直接访问/var/lambda/data目录
```

# 节点惩罚
验证节点在以下情况下会被惩罚，并扣除节点质押的TBB

1.对块进行双签，惩罚为  
- 扣除 1% 质押的TBB  
- 监禁三天  
（注意不要让节点出现双签情况！！！）  
双签场景：不同机器使用同一`priv_validator_key.json`文件启动节点  

2.在最近的10000个块中对少于500个块签名(掉线1天左右)，惩罚为  
- 扣除 0.01% 质押的TBB   
- jail 10分钟   

# 重新加入共识网络
1.验证节点最低质押要求`666,666,666utbb`,  如果低于需要发起质押补足扣除的utbb.

质押代币命令示例参考
``` 
./lambdacli tx staking delegate [validator-address] [amount-of-utbb] --from [your-account-name]
```
2.发起unjail消息来重新加入共识网络(每10分钟只能发起一次unjail命令)
```
./lambdacli tx slashing unjail *--from [your-account-name]*
```
