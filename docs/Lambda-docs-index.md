# Lambda 主网挖矿全解析

## Lambda 存储网络简介
Lambda 存储网络主要由共识网络、存储网络和去中心化的存储交易市场构成。共识网络是由验证节点（Validator）运行，通对存储矿工数据存储验证和验证节点矿池TBB质押机制完成共识。存储网络由存储矿工组成（StorageMiner），存储矿工负责存储用户数据，并位数数据安全，获得存储挖矿奖励，存储交易市场（Marketplace）由存储做市商创建，为存储矿工和用户间提供存储交易撮合。

## 文档前言
Lambda 主要角色由验证节点、存储矿工、存储做市商构成及他们的职责和收益模式，进一步熟悉了解 Lambda 共识网络。

除此之外，此文档将一步一步引导用户，从熟知 Lambda 生态角色、职责和收益模式，到如何加入共识网络获取收益，文档中涵盖了所有成为生态角色的前期准备，中期维护，后期收益等细化内容。

如果此前对 Lambda 生态及经济模型有一定了解的用户，可通过此文档加深对 Lambda 共识网络的理解。如果您初次接触 Lambda 是新人，那么您可以同时参阅 [Lambda 钱包使用手册](Lambda-Wallet-Guide.md) 以了解如何在支持的平台上安装 Lambda 钱包。

## 一、验证节点（Validator）
验证节点主要职能为维护共识网络、打包、出块、验证存储矿工提交的时空证明（POST），任何人都可以通过质押667个TBB成为验证节点，TBB可通过交易市场购买（目前kangbo.io支持TBB的交易），或使用钱包（[Lambda 主网钱包](https://www.lambdastorage.com/walletpages)）中的主网 LAMB 进行兑换 [查看兑换教程](Lambda-Wallet-Guide.md) 。

## 二、如何成为验证节点？
### 1、验证节点前期准备

1）一个主网钱包地址，通过 [主网钱包](https://www.lambdastorage.com/walletpages) 生成；

2）钱包内需要有大于667个TBB；

3）一台服务器（[最低配置要求](Lambda-Validator-Mining.md)）

### 2、如何启动验证节点

参照（[Validator接入文档](Mainnet-Validator-Guide.md)）Validator接入文档启动节点即可。启动后可通过[浏览器](http://explorer.lambdastorage.com/#/)、或[状态&监控系统](http://stats.lambdastorage.com/)查看节点状态。

节点启动后请务必参照此文档进行备份（[备份和恢复节点签名文件](Mainnet-Validator-Keybackup.md)）接入过程中遇到问题可参考（[主网接入常见问题](FAQ.md)）。

### 3、验证节点收益

1）提高该节点下矿工的TBB的质押量；

2）提高该节点下存储矿工实际存储数据量即存储算力；

3）保持节点稳定，持续获得区块打包奖励；

验证节点详细收益模型参考 [《Lambda经济白皮书》](https://www.lambdastorage.com/doc/Lambda%E7%BB%8F%E6%B5%8E%E7%99%BD%E7%9A%AE%E4%B9%A6.pdf) 、[《Lambda 经济模型参数》](https://talk.lambdastorage.com/hc/zh-cn/articles/360011349758-Lambda-%E7%BB%8F%E6%B5%8E%E6%A8%A1%E5%9E%8B%E5%8F%82%E6%95%B0)。

## 三、存储矿工（StorageMiner）
存储矿工通过存储交易市场获得存储订单，并为客户保存数据，存储数据后即可形成存储算力，正常提交存储证明，即可获得存储挖矿奖励。任何人都可以通过申明容量后并提供存储空间，获得存储订单，生成存储算力成为一个矿工，简要过程为首先进行容量申明，即将来要提供多少存储空间，即质押TBB，每质押一个TBB即为申明了1TB的容量，申明容量后可以获得TBB的质押收益，申明容量后矿工启动矿机（[矿工接入文档](Lambda-Store-and-Mining.md)），生成算力。

## 四、存储挖矿和质押挖矿
### 如何存储挖矿？
#### 1、存储挖矿前期准备

1）选定矿池（验证节点）进行容量申明（质押TBB）；

2）部署存储矿机，一般采用存储池部署方式，即由MinerNode（MN）进行链上管理，多个StorageNode（SN）进行数据存储，即一个MN可管理多个SN；

3）需要公网可访问的地址（静态或动态公网IP地址）。

4）获得更多的存储订单

***注：存储矿工只进行容量申明那么只会获得TBB质押收益，进行容量申明后同时存储了有效数据，那么可获得质押收益和存储挖矿收益，提供的存储空间不一定与申明容量一致，如，可以申明 100T，只提供10T存储空间。***

#### 2、存储挖矿操作步骤

参照（[存储矿工接入教程](Lambda-Store-and-Mining.md)）存储矿工接入文档启动存储矿工。启动后可通过[命令行](lambdacli/README.md)、[主网钱包](https://www.lambdastorage.com/walletpages)、[浏览器](http://explorer.lambdastorage.com/#/)、或[状态&监控系统](http://stats.lambdastorage.com/)查看存储矿工状态。

#### 3、存储挖矿收益

1）可以获得申明容量的收益，即TBB质押的收益；

2）可以获得存储挖矿收益，即提供存储空间进行挖矿的收益；

3）可以获得用户支付的存储费用。

存储矿工收益模型参考 [《Lambda经济白皮书》](https://www.lambdastorage.com/doc/Lambda%E7%BB%8F%E6%B5%8E%E7%99%BD%E7%9A%AE%E4%B9%A6.pdf) 、[《Lambda 经济模型参数》](https://talk.lambdastorage.com/hc/zh-cn/articles/360011349758-Lambda-%E7%BB%8F%E6%B5%8E%E6%A8%A1%E5%9E%8B%E5%8F%82%E6%95%B0)。

### 如何质押挖矿？
#### 1、质押挖矿前期准备

1）创建主网钱包地址，通过[主网钱包](https://www.lambdastorage.com/walletpages)生成；

2）参照 [Lambda 钱包使用说明](Lambda-Wallet-Guide.md) 购买TBB 质押到选定的验证节点。

#### 2、质押挖矿收益

1）目前为总区块奖励的 50%，完成空间质押获取质押收益；

2）质押挖矿收益模型参考 [《Lambda经济白皮书》](https://www.lambdastorage.com/doc/Lambda%E7%BB%8F%E6%B5%8E%E7%99%BD%E7%9A%AE%E4%B9%A6.pdf)。

## 五、存储市场（Market）
任何人通过质押100万LAMB均可称为市场运营商，市场运营商可以定义市场规则《[市场质押操作手册》](Market-Delegate-Operation-Guide.md)，主要有几方面工作:

1）市场运营商可以面向最终用户运营自有业务，如物联网数据交换平台，

2）市场运营商通过额外激励矿工在该市场提供存储空间参照资产发行文档[《Lambda发行资产文档》](Asset-Manage-Guide.md) ，

3）市场运营商可以通过发行的资产与自有业务结合形成完整的业务生态，可以成为基于Lambda的链上链，可以自定义业务和自身资产的挖矿模型。

## 六、开发者（Developer）
任何对 Lambda 生态应用或区块链爱好者都可以通过开发项目方所要求的项目，按开发阶段获取最高 3000000 LAMB 对应比例的开发奖励，开发项目可按照 [Lambda 开发者悬赏计划](https://talk.lambdastorage.com/t/topic/290)中所提到的项目进行开发，开发者可参考 [Lambda 源代码](https://github.com/LambdaIM) 及[开发者应用开发指导](Application-Develop-Guide.md) 文档进一步了解，文档中包含了 Lambda 源代码、开发组件、资产发行与存储交易市场等功能，并持续为开发者更新最新内容。