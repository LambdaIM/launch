# 应用开发指导
## 配置环境

### 下载安装包
目前安装包仅支持Linux 环境
```
wget http://download.lambdastorage.com/lambda-storage/0.2.7_rc2/lambda-storage-0.2.7_rc2-testnet.tar.gz
```

### 配置客户端
配置客户端了链接的主网地址，以及区块链的chain-id

```   plain
mkdir -p ~/LambdaIM && cd ~/LambdaIM

tar zxvf lambda-storage-0.2.7_rc2-testnet.tar.gz && cd lambda-storage-0.2.7_rc2-testnet

./lambdacli config node tcp://bj1.testnet.lambdastorage.com:26657

./lambdacli config chain-id lambda-chain-test4.9

./lambdacli config trust-node true

```
* 测试网可选节点：
```   plain
./lambdacli config node tcp://bj1.testnet.lambdastorage.com:26657
./lambdacli config node tcp://bj2.testnet.lambdastorage.com:26657
./lambdacli config node tcp://bj3.testnet.lambdastorage.com:26657
./lambdacli config node tcp://bj4.testnet.lambdastorage.com:26657
```
* 主网可以选择的节点
```
需要自己链接验证节点所要验证节点地址和端口号
或自己搭建运行验证节点程序并同步数据

```

### 创建用户并保存助记词

涉及生成账户相关、签名相关算法说明 http://docs.lambda.im/Wallet-Hdkey/


*助记词是用来恢复帐户信息的需谨慎保存

```   plain
./lambdacli keys add user1
```
输出结果
```   plain
Enter a passphrase to encrypt your key to disk:
Repeat the passphrase:
NAME:	TYPE:	ADDRESS:					PUBKEY:
user1	local	lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6	lambdapub1addwnpepqdjpeayr7xf7cn74n3t7hcnt6567qlwune7g5uf008qsak4yd60qczc9ulg
**Important** write this mnemonic phrase in a safe place.
It is the only way to recover your account if you ever forget your password.
##保存助记词
year bag cupboard tiny whip street want lake rabbit gesture father obvious index xx xxxx scrap convince xxx elegant hood rent luggage forward trade
```
1. 获得lamb测试币

测试网水龙头: 

[http://faucet.lambdastorage.com/](http://faucet.lambdastorage.com/)

查询lamb余额：

```   plain
./lambdacli query account lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
```
输出结果：
```   plain
Account:
  Address:       lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
  Pubkey:
  Coins:         100000000000ulamb
  AccountNumber: 486
  Sequence:      0
```
* lambda 区块链中的最小单位为u, 1lamb = 1000000ulamb

## 发行资产(可选)

创建一个pig币用作存储的支付, 资产最小单位也是u，创建资产需要抵押1000000lamb币。

### 创建资产

```   plain
./lambdacli tx asset create 100000000000000upig 1000000000000ulamb --asset-name "pig Coin" --mintable --from lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6  --broadcast-mode block
```
输出结果：
```   plain
{"chain_id":"lambda-chain-test4.9","account_number":"485","sequence":"0","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgCreateAsset","value":{"address":"lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6","asset":{"denom":"upig","amount":"100000000000000"},"token":{"denom":"ulamb","amount":"1000000000000"},"name":"pig Coin","mintable":true}}],"memo":""}
confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'master':
Response:
  Height: 460520
  TxHash: 84B01755F40A0EB98CF621DBA230CE4A14AF91BC7CE991340672B3BA71D3EC58
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 49903
  Tags:
    - action = createAsset
    - address = lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
    - name = pig Coin
    - symbol = upig
    - amount = 100000000000000
    - mintable = true
```
### 查看资产

```   plain
./lambdacli query account 
 lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
```
输出结果：
```   plain
Account:
  Address:       lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
  Pubkey:        lambdapub1addwnpepqdjpeayr7xf7cn74n3t7hcnt6567qlwune7g5uf008qsak4yd60qczc9ulg
  Coins:         1000000000000ulamb,100000000000000upig,1000000000utbb
  AccountNumber: 485
  Sequence:      1
```
### 转帐

```   plain
./lambdacli tx send  lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8 100000000upig --from user1
```
输出结果：
```   plain
{"chain_id":"lambda-chain-test4.9","account_number":"485","sequence":"1","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"cosmos-sdk/MsgSend","value":{"from_address":"lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6","to_address":"lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8","amount":[{"denom":"upig","amount":"100000000"}]}}],"memo":""}
confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'master':
Response:
  TxHash: 680CC553CD23CC6951865C97635691F1FA1D35A669E5A12BF83DFF025C5D2F0E
```
### 查询交易
需要注意的是，logs中的success为true，说明交易成功了

```   plain
./lambdacli query tx 680CC553CD23CC6951865C97635691F1FA1D35A669E5A12BF83DFF025C5D2F0E -o json
```
输出结果：
```   plain
{
  "height": "460638",
  "txhash": "680CC553CD23CC6951865C97635691F1FA1D35A669E5A12BF83DFF025C5D2F0E",
  "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
  "logs": [
    {
      "msg_index": "0",
      "success": true,
      "log": ""
    }
  ],
  "gas_wanted": "200000",
  "gas_used": "28486",
  "tags": [
    {
      "key": "action",
      "value": "send"
    },
    {
      "key": "sender",
      "value": "lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6"
    },
    {
      "key": "address",
      "value": "lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6"
    },
    {
      "key": "recipient",
      "value": "lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8"
    },
    {
      "key": "address",
      "value": "lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8"
    }
  ],
  "tx": {
    "type": "auth/StdTx",
    "value": {
      "msg": [
        {
          "type": "cosmos-sdk/MsgSend",
          "value": {
            "from_address": "lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6",
            "to_address": "lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8",
            "amount": [
              {
                "denom": "upig",
                "amount": "100000000"
              }
            ]
          }
        }
      ],
      "fee": {
        "amount": null,
        "gas": "200000"
      },
      "signatures": [
        {
          "pub_key": {
            "type": "tendermint/PubKeySecp256k1",
            "value": "A2Qc9IPxk+xP1ZxX6+Jr1TXgfdyefIpxL3nBDtqkbp4M"
          },
          "signature": "wZkaj51BfeXgZGNlOeehv/d00PWDFJkLyLj/viB1HSIuCXVg2GS1H25jczh/kcA8BRnidVCbeqI+7A8QYwDeGw=="
        }
      ],
      "memo": ""
    }
  },
  "timestamp": "2020-05-12T05:29:32Z"
}
```
### 资产API

测试网节点列表：

```   plain
bj1.testnet.lambdastorage.com:13659
bj2.testnet.lambdastorage.com:13659
bj3.testnet.lambdastorage.com:13659
bj4.testnet.lambdastorage.com:13659
```

主网节点列表
```
需要自己链接验证节点所要验证节点地址和端口号
或自己搭建运行验证节点程序并同步数据
```
#### 查询 账户资产

/auth/accounts/{address}

测试接口：

```   plain
http://bj1.testnet.lambdastorage.com:13659/auth/accounts/lambda1v664znyhztfx3m0v0uua497r5cptg3rd2ytnm8
```
返回结果：
```   javascript
 //查找coins 中denom 为 ulamb 即可
{
    "type": "auth/Account",
    "value": {
        "address": "lambda1v664znyhztfx3m0v0uua497r5cptg3rd2ytnm8",
        "coins": [{
            "denom": "ubtc",
            "amount": "1000000"
        }, {
            "denom": "ulamb",
            "amount": "3000000"
        }],
        "public_key": null,
        "account_number": "502",
        "sequence": "0"
    }
}
```
#### 查询交易

txs/{txhash}

测试接口：

```   plain
http://bj1.testnet.lambdastorage.com:13659/txs/680CC553CD23CC6951865C97635691F1FA1D35A669E5A12BF83DFF025C5D2F0E
```
返回结果：
```   json
{
  "height": "460638",
  "txhash": "680CC553CD23CC6951865C97635691F1FA1D35A669E5A12BF83DFF025C5D2F0E",
  "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
  "logs": [
    {
      "msg_index": "0",
      "success": true,
      "log": ""
    }
  ],
  "gas_wanted": "200000",
  "gas_used": "28486",
  "tags": [
    {
      "key": "action",
      "value": "send"
    },
    {
      "key": "sender",
      "value": "lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6"
    },
    {
      "key": "address",
      "value": "lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6"
    },
    {
      "key": "recipient",
      "value": "lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8"
    },
    {
      "key": "address",
      "value": "lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8"
    }
  ],
  "tx": {
    "type": "auth/StdTx",
    "value": {
      "msg": [
        {
          "type": "cosmos-sdk/MsgSend",
          "value": {
            "from_address": "lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6",
            "to_address": "lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8",
            "amount": [
              {
                "denom": "upig",
                "amount": "100000000"
              }
            ]
          }
        }
      ],
      "fee": {
        "amount": null,
        "gas": "200000"
      },
      "signatures": [
        {
          "pub_key": {
            "type": "tendermint/PubKeySecp256k1",
            "value": "A2Qc9IPxk+xP1ZxX6+Jr1TXgfdyefIpxL3nBDtqkbp4M"
          },
          "signature": "wZkaj51BfeXgZGNlOeehv/d00PWDFJkLyLj/viB1HSIuCXVg2GS1H25jczh/kcA8BRnidVCbeqI+7A8QYwDeGw=="
        }
      ],
      "memo": ""
    }
  },
  "timestamp": "2020-05-12T05:29:32Z"
}
```

#### 转帐

##### 获取chain-id

```   plain
/node_info
```
测试接口：
```   plain
http://bj1.testnet.lambdastorage.com:13659/node_info
```
返回结果：
```   json
{
  "protocol_version": {
    "p2p": "7",
    "block": "10",
    "app": "0"
  },
  "id": "e02882af5bdafa5aec086c32b8398c268d2337f1",
  "listen_addr": "bj1.testnet.lambdastorage.com:26656",
  "network": "lambda-chain-test4.9", //chain-id
  "version": "0.5.0-goleveldb",
  "channels": "4020212223303800",
  "moniker": "cv-moniker-1",
  "other": {
    "tx_index": "on",
    "rpc_address": "tcp://0.0.0.0:26657"
  }
}
```
##### 获得用户sequence

```   plain
/auth/accounts/{address}
```
测试接口：
```   plain
http://bj1.testnet.lambdastorage.com:13659/auth/accounts/lambda16cheh6j34ncyunwgfkq2940cs8222jka0fsp4k
```
输出结果：
```   json
{
  "type": "auth/Account",
  "value": {
    "address": "lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6",
    "coins": [
      {
        "denom": "ulamb",
        "amount": "999959200000"
      },
      {
        "denom": "upig",
        "amount": "99999900000000"
      }
    ],
    "public_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "A2Qc9IPxk+xP1ZxX6+Jr1TXgfdyefIpxL3nBDtqkbp4M"
    },
    "account_number": "485",   //取该值
    "sequence": "7"   //取该值
  }
}
```
##### 获取交易手续费(gas)

接口

```   plain
/bank/accounts/${senderAddress}/transfers
类型 post
发送数据类型 json
```
测试接口：
```   plain
http://bj1.testnet.lambdastorage.com:13659/bank/accounts/lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6/transfers
```
发送内容

```   json
{
    "base_req": {
        "sequence": "7", //填写该值
        "from": "lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6",//帐户
        "account_number": "485", //填写该值
        "chain_id": "lambda-chain-test4.9", //chain-id需填写
        "simulate": true,
        "memo": ""
    },
    "amount": [{
        "amount": "1000000", //数量u单位
        "denom": "ulamb"  //代币名称
    }],
    "from_address": "lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6",
    "to_address": "lambda16cheh6j34ncyunwgfkq2940cs8222jka0fsp4k"
}
```
返回结果：
```   plain
  {"gas_estimate":"28077"}
```
##### 对交易数据签名
签名前的数据结构
签名相关说明详细见 http://docs.lambda.im/Wallet-Hdkey/#2
```   json
{
    "account_number": "485",  //通过用户信息获取
    "chain_id": "lambda-chain-test4.9", //链的版本号 通过最新的区块信息获取 
    "fee": {//手续费
        "amount": [{
            "amount": "101745",
            "denom": "ulamb" 
        }],
        "gas": "40698"  //gas
    },
    "memo": "", //备注
    "msgs": [{
        "type": "cosmos-sdk/MsgSend", //交易类型
        "value": {
            "amount": [{
                "amount": "1000000",   //交易的数量
                "denom": "ulamb"    //交易的代币类型
            }],
            "from_address": "lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt",  //发送地址
            "to_address": "lambda1hynqrp2f80jqs86gu8nd5wwcnek2wwd3esszg0"   //接受地址
        }
    }],
    "sequence": "7"  //通过获取用户信息接口获取
}
```
##### 发送交易

接口

```   plain
/txs
```
测试接口
```   plain
http://bj1.testnet.lambdastorage.com:13659/txs
类型 post
发送数据类型 json
```
发送内容

```   plain
{
    "tx": {
        "msg": [{
            "type": "cosmos-sdk/MsgSend",
            "value": {
                "amount": [{
                    "amount": "1000000", //转帐1lamb
                    "denom": "ulamb"
                }],
                "from_address": "lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt",
                "to_address": "lambda1hynqrp2f80jqs86gu8nd5wwcnek2wwd3esszg0"
            }
        }],
        "fee": {
            "amount": [{
                //amount = gas * gas price
                //gas price 设置为0.025ulamb, 调整该值可调整手续费大小
                "amount": "701", 
                "denom": "ulamb"
            }],
            "gas": "28077" //获得的gas价格
        },
        "signatures": [{  
            "signature": //签名的结果
"fa9bUlNRA3qa9PEYR2py6CgpQbbqVsuKhJRowMdlf90byj7M/2B1YQsu6EPAk1V/tLkKiNwEadkAKNFUxZngGA==",
            "pub_key": {
                "type": "tendermint/PubKeySecp256k1",
                "value": "AjmQ01Z+IoHuKLdPaFzV6IJQB88ahW2qv2rEw2H4B5dq"  //公钥
            }
        }],
        "memo": ""
    },
    "mode": "block"    发送交易的方式async 为异步，block 为同步
}
```
### 全部区块链API

[http://docs.lambda.im/api-reference/paths/](http://docs.lambda.im/api-reference/paths/)

## 存储矿工接入(自建存储空间卖方)

[http://docs.lambda.im/Testnet-Miner-Guide/](http://docs.lambda.im/Testnet-Miner-Guide/)

## 购买资产市场的空间（仅限测试网）

在浏览器中可以找到一个矿工的矿工操作地址
```
lambdacli tx dam user buy --duration 1month --size 101GB --ask-address lambdamineroper1zm99mael4ef9u9qcyjnwsrp59sua9943y6w23e --asset uxxb --from user1
```
lambdamineroper1zm99mael4ef9u9qcyjnwsrp59sua9943y6w23e 为矿工操作地址
## 购买空间


### 查询矿工出售的空间 （购买lambda市场的空间）

```   plain
./lambdacli query market miner-sellorders  lambda1r3my74gqyt8zfgqu358nv86nqncxu34cs0ek44 1 100
```
输出结果：
```   plain
ID                                         PRICE    RATE     TOTAL    AVAIABLE STATUS   CREATE_TIME          MIN_BS   MIN_BT   MAX_BT   ADDR
1951F346F2A1AC19DE282ACF3557DA14D54001D1   5LAMB    1.00     1024     0        1        2020-03-06,13:16:48  1        90DAYS   1800DAYS lambdamineroper1r3my74gqyt8zfgqu358nv86nqncxu34cyq43qg
3BD7E4142C2BD393E1EF3FF983D49758F99F8178   5LAMB    1.00     1024     0        1        2020-03-04,11:59:22  1        30DAYS   1800DAYS lambdamineroper1r3my74gqyt8zfgqu358nv86nqncxu34cyq43qg
4EACCB414C75DBE73B897F452D7BA76DA9FA6011   5LAMB    1.00     1024     0        1        2020-03-20,10:04:35  4        120DAYS  1320DAYS lambdamineroper1r3my74gqyt8zfgqu358nv86nqncxu34cyq43qg
806326624BE6764.974CFF229B8FF30C37F658A0   5LAMB    1.00     500      0        1        2020-04-23,06:15:37  10       360DAYS  360DAYS  lambdamineroper1r3my74gqyt8zfgqu358nv86nqncxu34cyq43qg
9F491F6FE92D664798E774DCFD77F64828B47756   5LAMB    1.00     1024     0        1        2020-03-04,11:05:50  1024     30DAYS   1800DAYS lambdamineroper1r3my74gqyt8zfgqu358nv86nqncxu34cyq43qg
C516EF2E4778E6078D87949E582C245B4D2CBBF5   5LAMB    1.00     1024     0        1        2020-03-11,08:46:12  1        90DAYS   360DAYS  lambdamineroper1r3my74gqyt8zfgqu358nv86nqncxu34cyq43qg
```
卖单列描述：
| Field   | Description   |
|:----|:----|
| NODE   | show node status with Online or Offline   |
| ID   | sell order id   |
| MIN_BS   | Minimum purchase space   |
| MIN_BT   | Minimum purchase time   |
| MAX_BT   | Maximum purchase time   |
| ADDR   | Miner Address   |

### 购买空间

从矿工出售空间订单中购买5G空间时间为1个月：

```   plain
./lambdacli tx market create-buyorder --duration 1month --market-name lambdamarket --size 5GB --from user1 --broadcast-mode block --sellorder-id 761E89B5CA7D2988D72F3F2FC5AC4CDD10DDDCC1
```
输出结果：
```   plain
{"chain_id":"lambda-chain-test4.9","account_number":"485","sequence":"6","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgCreateBuyOrder","value":{"address":"lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6","duration":"2592000000000000","size":"5","sellOrderId":"761E89B5CA7D2988D72F3F2FC5AC4CDD10DDDCC1","marketName":"lambdamarket"}}],"memo":""}
confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'user1':
Response:
  Height: 461738
  TxHash: 92B748DF4956A86E7948942ACE1FDFA5965E85D037E37A8B5901DE8069C517B1
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 55745
  Tags:
    - action = createBuyOrder
    - address = lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
    - orderId = 60E003E7414DEEF9A7C5F89997980CE7666EF220
    - buyOrder = 0a283630453030334537343134444545463941374335463839393937393830434537363636454632323012149372c8fe27338c648289684dac33aaea1261db881a013520808088ba90adcd042a110a05756c616d62120834303030303030303228373631453839423543413744323938384437324633463246433541433443444431304444444343313a283432304346414645413538424545413439313843433834454233393933383141463745343445453642145de544b0ed7b6178f73dfdc26d976c41a49b9fd04a0c08a197e9f50510e2d1d8f202
    - matchOrder = 0a28343230434641464541353842454541343931384343383445423339393338314146374534344545361214d6ec7497354fa3d5640f9d15ce1bc1b031fc73301a149372c8fe27338c648289684dac33aaea1261db882228373631453839423543413744323938384437324633463246433541433443444431304444444343312a28363045303033453734313444454546394137433546383939393739383043453736363645463232303207383030303030303a0135420c08a197e9f50510e2d1d8f2024a0c08a1b187f70510e2d1d8f2025080c0e285e3685a0c08a197e9f50510e2d1d8f2026a145de544b0ed7b6178f73dfdc26d976c41a49b9fd072110a05756c616d62120834303030303030307a110a05756c616d6212083430303030303030
```
### 查询订单

```   plain
./lambdacli query market  matchorders lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6 1 100
```
输出结果：
```   plain
MatchOrder
  OrderId:               420CFAFEA58BEEA4918CC84EB399381AF7E44EE6
  AskAddress:            lambdamineroper16mk8f9e4f73a2eq0n52uux7pkqclcuesww60qj
  BuyAddress:            lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
  SellOrderId:           761E89B5CA7D2988D72F3F2FC5AC4CDD10DDDCC1
  BuyOrderId:            60E003E7414DEEF9A7C5F89997980CE7666EF220
  Price:                 8000000
  Size:                  5
  CreateTime:            2020-05-12 07:09:21.7773984.9 +0000 UTC
  EndTime:               2020-06-11 07:09:21.7773984.9 +0000 UTC
  CancelTimeDuration:    1h0m0s
  WithDrawTime:          2020-05-12 07:09:21.7773984.9 +0000 UTC
  Status:                0
  MarketAddress:         lambdamarketoper1thj5fv8d0dsh3aealhpxm9mvgxjfh87srk3887
  UserPay:               40000000ulamb
  MinerPay:              40000000ulamb
  PeerId:
  DhtId:                 5CS8tUKpcjkEtB3VbJgCwoEL3G4W39G4yC2LYF15ft3q
```
## 存储业务

lambda storage目前提供了两个版本的 兼容部分s3接口的 gateway：

* s3gateway  针对于单个订单的gateway，主要是方便用户迁移数据，将其他支持存储的数据，通过s3迁移到lambda
* lambgw       针对多个订单的gateway，适用于有更多业务需要的应用开发者，也支持s3接口上传下载文件

### 关于ui和订单的说明
s3gateway 自带的UI是可用的，启动后可以创建Bucket
lambgw  订单id映射为Bucket，不支持创建Bucket，目前再带的ui不可用，

s3gateway 的启动命令如下
```
./storagecli s3gw run --account user1 --broker.extra_order_id  ${匹配订单的id}  --debug
```



本文档仅对lambgw进行说明。

### 使用lambgw开发应用须知

目前lambgw支持：

* lambda存储网络的多订单(体现为多个bucket)
* 常驻服务
* 接口更新订单信息
* 身份管理




不支持：

* S3  multipart api, 可以通过客户端参数调整multipart_threshold来避免使用



#### 使用方式 1（推荐）

开发者使用自己的文件上传下载api 中转文件到 lambgw。

开发者需要：

* 使用自己的文件上传下载api接收文件，然后中转到lambgw
* 管理文件映射
* 控制应用订单相关的业务
* 管理应用的用户



部署方式：

* 公网暴露应用的api
* 内网 与 lambgw 通信，只用一份accesskey(配置文件配置)
* 用户只调用应用api



#### 使用方式 2（待确定）

开发者只开发订单、用户相关的业务， 但是直接使用s3api通过lambgw来传输文件。

这种情况下：

* lambgw支持可以分配带权限的accesskey
* 开发者需要将自己的用户绑定对应的lambgw accesskey(购买订单时需要更新权限)
* 开发者控制用户存储使用量(因为没有数据中转，这部分控制只能做到应用的客户端)
* 开发者控制订单映射(我们认为 订单映射 是应用的业务数据，lambgw应该只负责验证权限和存储)



部署方式：

* 公网 暴露 应用 api
* 公网 暴露 lambgw
* 用户需要调用 两套 api， 每个应用的用户使用自己的的accesskey



### 配置lambgw

初始化：

```   plain
wget http://download.lambdastorage.com/lambda-storage/0.2.7_rc2/lambda-storage-0.2.7_rc2-testnet.tar.gz
mkdir -p ~/LambdaIM && cd ~/LambdaIM
tar zxvf lambda-storage-0.2.7_rc2-testnet.tar.gz && cd lambda-storage-0.2.7_rc2-testnet
./storagecli init
```
默认链接的是主网

链接测试网
```
./storagecli init --testnet
```


配置s3端口与访问KEY：

```   
cat ~/.lambda_storagecli/config/user.toml
[gateway]
# 服务监听的地址
address = "127.0.0.1:9002"
# 用于访问服务的key
access_key = "accesskey"
secret_key = "secretkey"
```
启动后访问 127.0.0.1:9002，如果页面正常载入，配置就对了，如果打不开页面，需要检查address配置的ip和端口号


### 运行lambgw

```   shell
./storagecli lambgw run --account user1 --daemonize --log.file /tmp/gateway.log
```
--account 为购买空间的用户




#### 查看lambgw 的api调用日志

因为使用minio提供s3 api，受限于minio目前的日志查看方式，查看api调用日志可以使用：

`./storagecli lambgw admin trace --verbose`



#### lambgw运行中刷新订单

使用root accesskey（也就是配置文件中配置的accesskey）调用 `ListBucket`就会触发更新订单的操作，类似之前的`token sync`



### aws cli示例

安装[awscli](https://docs.aws.amazon.com/cli/latest/userguide/installing.html).

配置用于访问s3网关的key：

```   plain
$ aws configure
AWS Access Key ID [None]: accesskey
AWS Secret Access Key [None]: secretkey
Default region name [None]:
Default output format [None]:
```
配置multipart的阈值

```   shell
aws configure set default.s3.multipart_threshold 512MB
```



##### 上传文件

```   plain
aws s3 --endpoint=http://localhost:9002/ cp /path/to/your/file s3://ORDERID
```
##### 列出bucket内容

```   plain
aws s3 --endpoint=http://localhost:9002/ ls s3://ORDERID
```
##### 下载文件

```   plain
aws s3 --endpoint=http://localhost:9002/ cp s3://ORDERID/your-file /tmp/new-file
```

### api 上传文件

各语言sdk下载  https://docs.min.io/docs/javascript-client-quickstart-guide.html

```
var Minio = require('minio')

var minioClient = new Minio.Client({
  endPoint: '127.0.0.1',
  port: 8091,
  accessKey: 'lambda1',
  secretKey: '123456781',
  signature_version: 's3v4',
  useSSL: false,
});

// 读取Buckets 列表
minioClient.listBuckets(function (err, buckets) {
  if (err) return console.log(err)
  console.log('buckets :', buckets)
})

//创建bucket
minioClient.makeBucket('mybucket', '', function (err) {
  if (err) return console.log('Error creating bucket.', err)
  console.log('Bucket created successfully  ')
})

//上传文件
var fs = require('fs')
var file = './README.md'
var fileStream = fs.createReadStream(file)
var fileStat = fs.stat(file, function (err, stats) {
  if (err) {
    return console.log(err)
  }
  minioClient.putObject('mybucket', 'README.md', fileStream, stats.size, function (err, etag) {
    console.log('-----')
    return console.log(err, etag) // err should be null
  })
})

//下载文件
var size = 0;
var data = '';
minioClient.getObject('mybucket', 'README.md', function (err, dataStream) {
  if (err) {
    return console.log(err)
  }
  var myWriteStream = fs.createWriteStream('./README2.md')
  dataStream.pipe(myWriteStream);
  dataStream.on('data', function (chunk) {
    size += chunk.length
  })
  dataStream.on('end', function () {
    console.log('End. Total size = ' + size)
  })
  dataStream.on('error', function (err) {
    console.log(err)
  })

})
```
