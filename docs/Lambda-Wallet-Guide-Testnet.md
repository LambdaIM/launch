# Lambda测试网钱包使用说明
版本 0.6.66 

一个钱包支持创建和管理多个账户，支持语言有中文和英文。  
主网0.6.66钱包使用参考：[桌面钱包使用手册(主网)](Lambda-Wallet-Guide.md)



下载地址 ：  
[https://github.com/LambdaIM/launch/releases/tag/Wallet0.6.66](https://github.com/LambdaIM/launch/releases/tag/Wallet0.6.66)  
[http://download.lambdastorage.com/wallet/0.6.66/](http://download.lambdastorage.com/wallet/0.6.66/)


![avatar](img/wallethome@2x.png)

* [创建账号](#创建账号)
* [助记词导入到节点的程序包](#助记词导入到节点的程序包)
* [导入账号](#导入账号)
* [钱包首页说明](#钱包首页说明)
* [领取测试网测试币](#领取测试网测试币)
* [转账](#转账)
* [导出账号配置文件](#导出账号配置文件)
* [更换钱包链接的Validator节点](#更换钱包链接的Validator节点)
* [LAMB兑换TBB](#LAMB兑换TBB)
* [查看验证节点和质押](#查看验证节点和质押)
* [转质押](#转质押)
* [取消质押](#取消质押)
* [查看合伙人和质押](#查看合伙人和质押)
* [提取奖励](#提取奖励)
* [提取节点收益](#提取节点收益)
* [查看资产和交易资产](#查看资产和交易资产)
* [提案与存入押金和投票](#提案与存入押金和投票)
* [市场与买卖空间](#市场与买卖空间)
* [打开lambdaS3控制台](#打开lambdaS3控制台)
* [主网和测试网的切换](#主网和测试网的切换)
* [挖矿子账户创建导出导入](#挖矿子账户创建导出导入)
* [初始化矿工](#初始化矿工)
* [选择使用钱包身份角色](#选择使用钱包身份角色)
* [挖矿向导](#挖矿向导)
* [设置gas价格](#设置gas价格)
* [提取订单佣金](#提取订单佣金)
* [订单续期](#订单续期)
* [市场质押](#市场质押)
* [提取市场质押收益](#提取市场质押收益)
* [聚合挖矿市场介绍](#聚合挖矿市场介绍)
* [聚合挖矿资产相关操作](#聚合挖矿资产相关操作)
* [聚合挖矿算力相关操作](#聚合挖矿算力相关操)




## 切换语言

![avatar](img/lang@2x.png)
## 账号创建和导入
### 创建账号
点击 Create Wallet  进入创建钱包的页面

输入钱包名称，密码，确认钱包密码，点击 Create 按钮，

![avatar](img/create@2x.png)

点击 Create按钮后，进入助记词页面


请妥善保管助记词，以便以后恢复钱包，点击Next Step进入下一页
最好在纸片上记录下助记词，助记词也可以导入到节点程序中。

![avatar](img/word@2x.png)

在确认助记词的页面，按照刚才显示的助记词顺序，点击页面上的单词

![avatar](img/select@2x.png)

点击完成后的页面

![avatar](img/selectall@2x.png)

点击 Export Keystore File  以便备份钱包。

![avatar](img/file@2x.png)

通过lambda**********.keyinfo可以再次导入钱包

通过钱包创建账号到此完成

### 助记词导入到节点的程序包

验证节点和矿工可以将钱包中的账号导入到挖矿程序包中(lambda chain)，运行挖矿程序

创建账号后，保存好助记词，助记词支持导入到验证节点和矿工的程序中

例如 助记词导入到节点的程序包

使用lambdacli调用命令行

```bash
./lambdacli keys add [name] --recover
```

根据提示两次输入密码

```bash
Enter a passphrase to encrypt your key to disk:
Repeat the passphrase:
```
![avatar](img/zhujici.png)


看到后面输出账户的地址如果和钱包一致，则表示导入成功

**tips**
注意，示例里面的助记词组合只是一个用例账户



### 导入账号

点击首页 import wallet  进入导入账号的页面

![avatar](img/import@2x.png)   

点击 Choose Wallet Files 选择账号的备份文件

备份文件后缀为 keyinfo,例如钱包创建的配置文件为lambda.keyinfo

输入创建钱包时候的密码，再输入新的钱包的名称，点击 import ,即可导入钱包

## 钱包首页说明
新创建的账号，余额为0，也没有交易记录

![avatar](img/home2@2x.png)  

顶部是导航菜单，点击设置按钮进入设置页面，点击账号地址可以复制账号

底部是钱包连接的Validator 节点的信息，包含节点的公钥地址，区块的高度，出块时间

账号有了交易记录的效果图

![avatar](img/home@2x.png)

## 领取测试网测试币

登录钱包账户后，点击首页的活动链接
![avatar](img/WXceshicoin1.png)
跳转到 
[http://faucet.lambda.im/](http://faucet.lambda.im/)
![avatar](img/WXceshicoinget.png)
输入 创建的lambda主网地址，例如 lambda163q4m634nq8les4nuvdvz49tk6aeh926t0**** 

现在支持 领取测试网的LAMB和TBB,用以进行存储挖矿测试

领取规则：  
一个IP每天可以领取50000个LAMB,5个TBB；  
一个lambda主网地址，可以领取10次LAMB和TBB



## 转账
点击首页的 Transfer 按钮 ，弹出转账对话框，填写转账的地址和金额

![avatar](img/send@2x.png)

点击下一步，预览交易信息，可以修改gas
![avatar](img/send3@2x.png)
点击确定。弹出输入钱包密码的对话框，输入钱包密码

![avatar](img/pasword@2x.png)

点击Submit，等待10s左右转账完成,转账成功效果如下

![avatar](img/ok@2x.png)

点击View Detail 查看转账详情

![avatar](img/view@2x.png)

## 导出账号配置文件

在设置页面点击 Keystore File Backup,即可查看账号备份文件

![avatar](img/set@2x.png)

## 更换钱包链接的Validator节点
在设置页面点击 Switch Validator 进入 查看Validator信息的页面

![avatar](img/info@2x.png)

在输入框里面更改节点的IP地址,点击 Submit，切换成功后提示信息如下 

![avatar](img/ok2@2x.png)


## LAMB兑换TBB

TBB可用于质押

![avatar](img/duihuan1@2x.png)

![avatar](img/duihuan2@2x.png)



## 质押相关操作
### 查看验证节点和质押
![avatar](img/valist@2x.png)
第一列 我的质押列表
第二列 验证节点列表
点击到验证节点 列表
![avatar](img/valist2@2x.png)
点击查看验证节点详细信息
![avatar](img/vainfo@2x.png)
点击质押按钮进行质押
![avatar](img/zhiyainfo@2x.png)

### 转质押
在节点的详情页面点击转质押按钮
![avatar](img/WXrv1@2x.png)
点击即可打开转质押窗口

填写需要转质押多少tbb，选择新的节点即可

（如果要转全部tbb，可能会失败，建议质押总量-0.1 个tbb 转质押比较容易成功）

![avatar](img/WXr2@2x.png)
### 取消质押
在节点的详情页面点击取消质押按钮
![avatar](img/cancel1@2x.png)
点击即可打开取消质押窗口
![avatar](img/cancel2@2x.png)
填写需要取消质押多少tbb

（如果要取消全部tbb，可能会失败，建议质押总量-0.1 个tbb 取消质押比较容易成功）


### 查看合伙人和质押
第一列 我的质押
第二列 合伙人列表
![avatar](img/plist@2x.png)
点击合伙人列表 查看全部的合伙人信息
![avatar](img/plist2@2x.png)
点击查看合伙人详情
![avatar](img/pinfo@2x.png)
点击质押按钮可以进行质押
![avatar](img/zhiya2@2x.png)

## 提取奖励相关操作
### 提取奖励
在首页点击【提取奖励】下拉菜单中的【提取奖励】
![avatar](img/wv3@2x.png)
![avatar](img/wi1@2x.png)


### 提取节点收益
在首页点击【提取奖励】下拉菜单中的【提取节点收益】
![avatar](img/wv1@2x.png)
即可打开提取节点收益的窗口
![avatar](img/wv2@2x.png)


### 查看资产和交易资产
在钱包首页点击资产标签，可以查看当前账户下有哪些资产
![avatar](img/asset1@2x.png)
点击交易按钮可以打开交易资产的窗口
![avatar](img/asset2@2x.png)

## 提案与存入押金和投票
点击顶部的导航菜单中的【提案】，即可进入提案列表页面
![avatar](img/t1@2x.png)
点击提案的的文字描述部分进入提案详情页面
![avatar](img/t2@2x.png)

提案状态为【押金阶段】时，可以给提案存入押金
点击存入押金按钮打开存入押金对话框
![avatar](img/t3@2x.png)
当存入总押金满足要求后，提案会进入【投票阶段】，点击投票按钮打开投票对话框

![avatar](img/t4@2x.png)
投票可以选择 同意 、反对、强烈反对、弃权

如果第一次投票投错了，没关系第二次投票会覆盖第一次投票的结果

投票的权重等于质押量，在节点质押和在合伙人质押都是有效质押

如果没有质押过，投票无效

## 市场与买卖空间

点击导航栏的市场链接进入市场页面


### 我的订单列表 
订单列表包含买单和卖单

![avatar](img/WXmk1@2x.png)

购买空间 

购买空间有两种方式：一种是自动匹配购买，一种是选择某一个矿工优质卖单购买。

自动匹配购买的是赔率为0.5单价为5lamb的普通卖单。

优质卖单是赔率为1单价大于5lamb的卖单，可指定购买。

![avatar](img/WXmk2@2x.png)

自动匹配购买空间只需要填写空间的大小和时长，例如购买3个月 2GB的空间

![avatar](img/WXmk7@2x.png)

购买矿工的优质买单需要先选择一个矿工，查看订单的最低购买空间大小、最短购买时长、最长时长是否满足自己的需求， 如果满足，填写空间大小和时长即可购买

![avatar](img/WXmk15@2x.png)


### 出售空间
 如当前账户是矿工账户，这里会列出这个账户在市场中挂的卖单列表
 
![avatar](img/WXmk3@2x.png)
在矿工管理程序中完成矿工和存储节点的启动后，可以在钱包中挂存储节点的卖单


在弹出的对话框中选择存储节点，填写要卖的空间大小（一个存储节点只能挂一个卖单，建议一次出售全部空间）

、赔率、单价 还有限制用户购买的条件，最小购买的空间大小、最短时长、最长时长 即可

关于赔率
赔率=0.5不能指定价格，只能是5LAMB/G/month

赔率=1需要指定价格,价格>=5LAMB/G/month

赔率=0.5为普通卖单,赔率>=1为优质卖单

只有优质卖单会出现在市场的列表里面，供用户选择，普通卖单只能进行自动匹配


![avatar](img/marketd4.png)





 在订单列表页面点击 查看详情进入订单的详情页面
 
 卖单的详情页面
 
![avatar](img/WXmk4@2x.png)


## 打开lambdaS3控制台
购买订单后，可以通过lambdaS3控制台来进行文件的上传下载，使用存储空间

![avatar](img/markets2.png)
这里可以修改登录s3 需要的用户名和密码

如果需要使用这个订单的空间，可以在lambda storage中上传文件到空间和删除空间中的文件

在订单 详情页面 ，点击查看订单空间， 弹窗授权对话框，即可完成对这个订单的授权

![avatar](img/markets1.png)

在登录页面输入：

钱包中提示的的lambda storage 控制台登录信息:密钥：lambda， 私钥：12345678

完成登录

![avatar](img/WXs32@2x.png)

就可以上传文件了，将文件拖拽到文件列表区域即可上传文件

![avatar](img/WXs31@2x.png)

## 主网和测试网的切换


登录钱包后 点击页脚左侧的网络类型，进入节点选择页面

![avatar](img/WXqh@2x.png)

点击默认主网ip 再点击提交 可切换到主网

点击默认测试网ip 再点击提交  可切换到测试网

## 挖矿子账户创建导出导入

在钱包首页点击挖矿，向导，点击下一步，直到看到创建子账户模块

![avatar](img/sonaccount.png)

可以看到创建矿工子账户和导入按钮

### 创建子账户
点击创建子账户按钮，打开创建子账户弹窗

![avatar](img/sonaccountd1.png)

创建矿工子账户需要输入当前钱包的助记词和密码，输入备注方便记忆

也可以导入钱包或区块链程序导出的子账户

### 导入子账户
如果已有子账户json文件，可通过钱包导入子账户。如已进行上面创建子账户操作，可跳过此步。

点击导入按钮，打开导入子账户弹窗

![avatar](img/sonaccountd2.png)

导入子账户需要选择子账户的json文件和当前钱包的密码

### 导出子账户
如果需要在矿工管理程序或区块链程序中使用挖矿子账户，可以导出子账户

![avatar](img/sonaccountd3.png)

导出子账户需要输入当前钱包的密码

例如 在矿工管理程序中选择钱包导出的子账户
![avatar](img/sonaccountd5.png)

## 初始化矿工

点击导航菜单的挖矿向导，在挖矿向导页面点击下一步，直到看到初始化矿工模块
点击矿工初始化按钮，打开创建矿工弹窗
![avatar](img/minersetup.png)

创建矿工需要选择钱包中的子账户和部署矿工服务器的dhtid
可以在 矿工管理程序中获取一个矿工服务的 dhtid
例如

![avatar](img/marketd3.png)

## 选择使用钱包身份角色

第一次安装使用钱包会自动弹窗，之后需要切换身份，在设置页面点击角色的编辑按钮，就可以打开弹窗
![avatar](img/role.png)

选择不同的角色，使用的功能略有差异
#### 钱包用户
查看资产，转账，质押挖矿，提案投票，提取质押奖励

#### 购买空间的用户
查看资产，转账，质押挖矿，提案投票，购买空间，使用lambdas3，提取质押奖励

#### 矿工
查看资产，转账，质押挖矿，提案投票，市场买卖空间，挖矿向导，提取质押奖励，提取存储挖矿奖励

#### 验证节点
查看资产，转账，质押挖矿，提案投票 ，提取质押奖励，提取节点收益


## 挖矿向导
选择矿工角色使用钱包，可以在导航菜单里看到挖矿向导的的菜单

![avatar](img/MiningGuide.png)
挖矿向导 将矿工挖矿的步骤展示出来，
并且整理了挖矿过程中需要用到的钱包的功能、和矿工管理程序的说明

挖矿向导中包含钱包的功能有

1质押挖矿

2创建矿工子账户

3初始化矿工

4出售空间




## 设置gas价格

在设置页面点击 编辑gas价格，打开弹窗，即可设置gas的价格
![avatar](img/Gasprice.png)





## 提取订单佣金

钱包首页点击交易，点击提取订单佣金
![avatar](img/txlist2.png)

打开提取订单收益的弹窗
![avatar](img/Orderrevenue.png)
提取订单收益 是批量提取订单中的收益
每次提取100个订单的收益
如果订单比较多，可以尝试分页地区，例如提取第一页面，提取第二页，
提取规则如下

每100个订单为1页，订单数量比较多，页码可以填写1、2、3、4、5、6等

一次只能同时提取100个订单的收益

提取操作时间限制1小时提取一次
订单中的收益是24小时计算一次，如果未到24小时发起提取，提取到的金额为0

## 订单续期

订单的使用时间需要增加，可以通过订单续期实现，在订单详情页面，点击订单需求按钮，打开对话框
![avatar](img/ordertime.png)
续期的价格和购买空间时候相同，
订单到期后无法续期

## 市场质押
在首页点击市场质押按钮，即可打开市场质押说明页面

![avatar](img/Marketpledge.png)


只有用户创建的市场可以质押，默认的lambdamarket是不可以质押的

市场质押的最小金额 1,000 LAMB

允许在多个市场中质押

用户可以通过质押的方式参与用户创建的市场的运营。 

市场收益是挂单手续费、成单手续费、续期手续费组成。

市场中的每笔收入会按照市场质押比例来进行分配。

收益分配规则：

市场创建人收取市场收益10%

市场质押人按照质押比例分配剩余的90%（市场创建人也在分配集合中）

点击市场质押按钮，打开市场质押对话框，即可进行质押
![avatar](img/MarketpledgeModel.png)

## 提取市场质押收益

![avatar](img/Withdrawmarketrevenue.png)

在首页交易的下拉列表中点击提取市场收益，打开提取市场收益的对话框

选择质押的市场，即可点下一步，提取市场质押收益

![avatar](img/Withdrawmarketrevenuemodel.png)

## 聚合挖矿市场介绍

首页点击聚合挖矿进入聚合挖矿市场
![avatar](img/miner/jhome.png)

市场首页展示的信息有 资产总量，和算力总量，还有当前市场的状态
![avatar](img/miner/jinfo.png)

聚合挖矿实现了挖矿过程中有资产的出资产、有算力的出算力，一起挖矿分享收益

1:状态为资产收益率较高时，通过存入资产可以获取较多的收益。

2:状态为算力收益率较高时，通过提供算力可以获取较多的收益。

## 聚合挖矿资产相关操作

点击资产标签，切换到资产信息页面

![avatar](img/miner/jasserts.png)

列表展示当前存入的资产和未提取的收益

点击存入资产按钮，打开弹窗，输入金额，即可存入资产
![avatar](img/miner/jDeposit.png)

资产随时取出资产，点击取出资产按钮，打开弹窗，即可取出资产

![avatar](img/miner/jWithdrawal.png)

产生的收益也可以随时提取，点击取出资产按钮，打开弹窗，即可提取收益

![avatar](img/miner/jincome.png)

## 聚合挖矿算力相关操作

点击算力标签 切换到算力页面

页面列表展示数据为我的算力和未提取的收益
![avatar](img/miner/jpowerinfo.png)

点击提取收益按钮，打开弹窗
![avatar](img/miner/jpowerincome.png)

点击订单列表，切换到订单页面
![avatar](img/miner/jorderlist.png)
可以查看订单详情
![avatar](img/miner/jorderinfo.png)
如果订单有效期在一个月以内

可以点击订单续期，打开弹窗，可延长订单到期时间

![avatar](img/miner/jorderRenewal.png)









