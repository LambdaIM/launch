# 配置环境

## 配置客户端

```plain
wget http://download.lambdastorage.com/lambda/0.5.0/lambda-0.5.0-testnet.tar.gz
mkdir -p ~/LambdaIM && cd ~/LambdaIM
tar zxvf lambda-0.5.0-testnet.tar.gz && cd lambda-0.5.0-testnet
./lambdacli config node tcp://47.93.196.236:26657
./lambdacli config chain-id lambda-chain-test5.0
./lambdacli config trust-node true
```
*测试网可选节点：
```plain
./lambdacli config node tcp://47.93.196.236:26657
./lambdacli config node tcp://47.94.129.97:26657
./lambdacli config node tcp://39.105.148.217:26657
./lambdacli config node tcp://182.92.66.63:26657
```
## 创建用户并保存助记词

*助记词是用来恢复帐户信息的需谨慎保存

```plain
./lambdacli keys add user1
```
输出结果
```plain
Enter a passphrase to encrypt your key to disk:
Repeat the passphrase:
NAME:	TYPE:	ADDRESS:					PUBKEY:
user1	local	lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6	lambdapub1addwnpepqdjpeayr7xf7cn74n3t7hcnt6567qlwune7g5uf008qsak4yd60qczc9ulg
**Important** write this mnemonic phrase in a safe place.
It is the only way to recover your account if you ever forget your password.
#保存助记词
year bag cupboard tiny whip street want lake rabbit gesture father obvious index xx xxxx scrap convince xxx elegant hood rent luggage forward trade
```
1. 获得lamb测试币

测试网水龙头: 

[http://faucet.lambdastorage.com/](http://faucet.lambdastorage.com/)

查询lamb余额：

```plain
./lambdacli query account lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
```
输出结果：
```plain
Account:
  Address:       lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
  Pubkey:
  Coins:         100000000000ulamb
  AccountNumber: 486
  Sequence:      0
```
*lambda 区块链中的最小单位为u, 1lamb = 1000000ulamb

# 发行资产

创建一个pig币用作存储的支付, 资产最小单位也是u，创建资产需要抵押1000000lamb币。

## 创建资产

```plain
./lambdacli tx asset create 100000000000upig 1000000000000ulamb --asset-name "pig Coin" --mint-type inflated_mint --total-supply 100000000000000 --inflation 1000000 --adjust-rate 0.5 --adjust-period 10000 --max-adjust-count 5 --genesis-height 10000  --from master  --broadcast-mode block
```
参数说明：

| Name   | Type   | Required   | Default   | Description   | 
|:----|:----|:----|:----|:----|
| --asset-name   | string   | false   |    | Asset Full Name   | 
| --mint-type   | string   | true   |    | Asset mint type, options: not_mint/one_time_mint/inflated_mint   | 
| --total-supply   | int   | false   | 0   | Only for inflated_mint type, total supply is upper limit of asset supply   | 
| --inflation   | int   | false   | 0   | Only for inflated_mint type, the asset's initial inflation per height   | 
| --adjust-rate   | double   | false   | 0   | Only for inflated_mint type, the adjust rate about inflation   | 
| --adjust-period   | int   | false   | 0   | Only for inflated_mint type, adjust inflation when period reached   | 
| --max-adjust-count   | int   | false   | 0   | Only for inflated_mint type, if reached max adjust count, it won't adjust inflation anymore   | 
| --genesis-height   | int   | false   | 0   | Only for inflated_mint type, produce asset only if reached genesis height   | 
| --from   | string   | true   |    | Name or address of private key with which to sign   | 

输出结果：

```plain
{"chain_id":"lambda1","account_number":"0","sequence":"1","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgCreateAsset","value":{"address":"lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6","asset":{"denom":"upig","amount":"100000000000"},"token":{"denom":"ulamb","amount":"1000000000000"},"name":"pig Coin","mint_type":3,"total_supply":{"denom":"upig","amount":"100000000000000"},"inflation":"1000000","adjust_rate":"0.500000000000000000","adjust_period":"10000","max_adjust_count":"5","genesis_height":"10000"}}],"memo":""}
confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'master':
Response:
  Height: 3548
  TxHash: 29E4B16DBF0BCFD4EEEBDBDD4FE8AA49432E49F768BE733FD281CC49EC0C673A
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 52981
  Tags:
    - action = createAsset
    - address = lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
    - name = pig Coin
    - symbol = upig
    - amount = 100000000000
```
## 查看资产

```plain
./lambdacli query account 
 lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
```
输出结果：
```plain
Account:
  Address:       lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
  Pubkey:        lambdapub1addwnpepqdjpeayr7xf7cn74n3t7hcnt6567qlwune7g5uf008qsak4yd60qczc9ulg
  Coins:         998000000000000ulamb,100000000000upig,665999666000utbb
  AccountNumber: 0
  Sequence:      2
```
## 转帐

```plain
./lambdacli tx send  lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8 100000000upig --from user1
```
输出结果：
```plain
{"chain_id":"lambda-chain-test5.0","account_number":"485","sequence":"1","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"cosmos-sdk/MsgSend","value":{"from_address":"lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6","to_address":"lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8","amount":[{"denom":"upig","amount":"100000000"}]}}],"memo":""}
confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'master':
Response:
  TxHash: 680CC553CD23CC6951865C97635691F1FA1D35A669E5A12BF83DFF025C5D2F0E
```
## 查询交易

```plain
./lambdacli query tx 680CC553CD23CC6951865C97635691F1FA1D35A669E5A12BF83DFF025C5D2F0E -o json
```
输出结果：
```plain
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
## 资产API

测试网节点列表：

```plain
47.93.196.236:13659
47.94.129.97:13659
39.105.148.217:13659
182.92.66.63:13659
```
### 查询资产

/auth/accounts/{address}

测试接口：

```plain
http://47.93.196.236:13659/auth/accounts/lambda1v664znyhztfx3m0v0uua497r5cptg3rd2ytnm8
```
返回结果：
```javascript
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
### 查询交易

txs/{txhash}

测试接口：

```plain
http://47.93.196.236:13659/txs/680CC553CD23CC6951865C97635691F1FA1D35A669E5A12BF83DFF025C5D2F0E
```
返回结果：
```json
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

### 转帐

#### 获取chain-id

```plain
/node_info
```
测试接口：
```plain
http://47.93.196.236:13659/node_info
```
返回结果：
```json
{
  "protocol_version": {
    "p2p": "7",
    "block": "10",
    "app": "0"
  },
  "id": "e02882af5bdafa5aec086c32b8398c268d2337f1",
  "listen_addr": "47.93.196.236:26656",
  "network": "lambda-chain-test5.0", //chain-id
  "version": "0.5.0-goleveldb",
  "channels": "4020212223303800",
  "moniker": "cv-moniker-1",
  "other": {
    "tx_index": "on",
    "rpc_address": "tcp://0.0.0.0:26657"
  }
}
```
#### 获得用户sequence

```plain
/auth/accounts/{address}
```
测试接口：
```plain
http://47.93.196.236:13659/auth/accounts/lambda16cheh6j34ncyunwgfkq2940cs8222jka0fsp4k
```
输出结果：
```json
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
#### 获取交易手续费(gas)

接口

```plain
/bank/accounts/${senderAddress}/transfers
类型 post
发送数据类型 json
```
测试接口：
```plain
http://47.93.196.236:13659/bank/accounts/lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6/transfers
```
发送内容

```json
{
    "base_req": {
        "sequence": "7", //填写该值
        "from": "lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6",//帐户
        "account_number": "485", //填写该值
        "chain_id": "lambda-chain-test5.0", //chain-id需填写
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
```plain
  {"gas_estimate":"28077"}
```
#### 对交易数据签名

```json
{
    "account_number": "485",  //通过用户信息获取
    "chain_id": "lambda-chain-test5.0", //链的版本号 通过最新的区块信息获取 
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
#### 发送交易

接口

```plain
/txs
```
测试接口
```plain
http://47.93.196.236:13659/txs
类型 post
发送数据类型 json
```
发送内容

```plain
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
## 全部区块链API

[http://docs.lambda.im/api-reference/paths/](http://docs.lambda.im/api-reference/paths/)

# 创建数据交易市场

## 创建市场

```plain
 ./lambdacli tx dam market create pigmarket upig 1 --from master --broadcast-mode block
#输出结果
{"chain_id":"lambda1","account_number":"0","sequence":"2","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgCreateDigitalAssetMarket","value":{"address":"lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6","marketName":"pigmarket","assetName":"upig","exchangeRatio":"100"}}],"memo":""}
confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'master':
Response:
  Height: 3786
  TxHash: 8FD853C04EF8CFC7087CD06EE7E22BFD4BCD99A6FBE7079DEDE44CD90524575C
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 34122
  Tags:
    - action = createDigitalAssetMarket
    - address = lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
    - asset = upig
```
## 授权矿工挖矿权限

```plain
lambdacli tx dam market authorize uabc --from master --pubkey ./pubkey.json
```
pubkey.json格式

```plain
{
  "pub_key": {
    "type": "tendermint/PubKeyEd25519",
    "value": "Pyd/mJPIdBhtUDNerCZORLPv5Ovjf8/ujlNA+X5tMgE="
  }
}
```
# 创建矿工

## 给矿工转币

```plain
./lambdacli tx send  lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8 5000000utbb --from master
./lambdacli tx send  lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8 5000000upig --from master
./lambdacli tx send  lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8 5000000ulamb --from master
```
查询帐户余额：

```plain
./lambdacli query account lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8
Account:
  Address:       lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8
  Pubkey:
  Coins:         5000000ulamb,5000000upig,5000000utbb
  AccountNumber: 2
  Sequence:    
```
## 质押TBB声明存储容量

```plain
./lambdacli tx staking delegate lambdavaloper1jdev3l38xwxxfq5fdpx6cva2agfxrkug4dkhew 1000000utbb --from user1 --broadcast-mode block
{"chain_id":"lambda1","account_number":"2","sequence":"0","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgDelegate","value":{"delegator_address":"lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8","validator_address":"lambdavaloper1jdev3l38xwxxfq5fdpx6cva2agfxrkug4dkhew","amount":{"denom":"utbb","amount":"1000000"},"validator_type":1}}],"memo":""}
confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'user1':
Response:
  Height: 325
  TxHash: C8DE63D918C92DF5F118282E303159BF48A75C20AD4ACE94F27E3A5F73838AAD
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 83517
  Tags:
    - action = delegate
    - address = lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8
    - delegator = lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8
    - destination-validator = lambdavaloper1jdev3l38xwxxfq5fdpx6cva2agfxrkug4dkhew
```
## 创建LAMB矿工

```plain
./lambdacli tx market create-miner --dht-id DgHL9h3pWVSGVtMf3W6bMg1cXX37NtoHrYXxtNjYArbH --mining-address lambda1dz24czwyku6hs8k2vqf855ujujchlhahv4ts5l --from user1
```
输出结果：
```plain
{"chain_id":"lambda1","account_number":"2","sequence":"1","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgCreateMiner","value":{"address":"lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8","dhtId":"DgHL9h3pWVSGVtMf3W6bMg1cXX37NtoHrYXxtNjYArbH","miningAddress":"lambda1dz24czwyku6hs8k2vqf855ujujchlhahv4ts5l"}}],"memo":""}
confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'user1':
Response:
  Height: 877
  TxHash: EA61583C05B1C436E91BF9FA2913FF1694F879DE5C2493E759AAA4185867216E
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 32968
  Tags:
    - action = createMiner
    - address = lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8
    - size = 1000.000000000000000000

  Timestamp: 2020-07-07T04:30:28Z
```
## 质押新资产

```plain
./lambdacli tx dam miner pledge upig 1000G --order-price 1000000upig --from user1 --broadcast-mode block
```
## 查看矿工质押

```plain
./lambdacli query dam pledge-records lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8
DigitalAssetRecord
  assetName:           upig
  orderPrice:          1000000
  power:               0
  miningSize:          1.000000000000000000
  matchSize:           0.000000000000000000
  pledgeAsset:         100000
  lastRewardHeight:    0
  selfChallengeHeight: 0
  available:           true
```
# 存储矿工接入(自建存储空间卖方)

[http://docs.lambda.im/Testnet-Miner-Guide/](http://docs.lambda.im/Testnet-Miner-Guide/)

# 购买空间

## 查询矿工出售的空间

```plain
./lambdacli query dam pledge-records lambda1lxsnz2udquwhs7vm622m3rm552ghssvhqrefp8
```
输出结果：
```plain
DigitalAssetRecord
  assetName:           upig
  orderPrice:          1000000
  power:               0
  miningSize:          1.000000000000000000
  matchSize:           0.000000000000000000
  pledgeAsset:         100000
  lastRewardHeight:    0
  selfChallengeHeight: 0
  available:           true
```
## 购买空间

从矿工质押的空间中购买1G空间时间为1个月：

```plain
./lambdacli tx dam user buy --duration 1month --size 1GB --ask-address lambdamineroper1zm99mael4ef9u9qcyjnwsrp59sua9943y6w23e --asset upig --from master
```
输出结果：
```plain
Password to sign with 'master':
Response:
  Height: 88
  TxHash: A08F78CC55626A90294BF739330BFFA5CFF3539E7C81AB82A4B6FA2702235000
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 40672
  Tags:
    - action = damCreateBuyOrder
    - address = lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
    - miner = lambdamineroper1lxsnz2udquwhs7vm622m3rm552ghssvh5v4w56
    - asset = upig
    - cost = 1000000
    - matchOrderID = DBF382D80C392C00F83A0EB888243B2732FE6B1E
    - matchOrder = 0a28444246333832443830433339324330304638334130454238383832343342323733324645364231451204757069671a149372c8fe27338c648289684dac33aaea1261db882214f9a1312b8d071d78799bd295b88f74a2917841972a013130c0843d3a0c08a6bb90f80510e89d83bf01420c08a6d5aef90510e89d83bf014a0c08a6bb90f80510e89d83bf01520f0a0475706967120731303030303030
```
## 查询订单

```plain
./lambdacli query dam all-match-orders lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6 1 100
```
输出结果：
```plain
Dam MatchOrder
  OrderID:               DBF382D80C392C00F83A0EB888243B2732FE6B1E
  Asset:                 upig
  BuyAddress:            lambda1jdev3l38xwxxfq5fdpx6cva2agfxrkugrflur6
  AskAddress:            lambdamineroper1lxsnz2udquwhs7vm622m3rm552ghssvh5v4w56
  DhtID:                 DgHL9h3pWVSGVtMf3W6bMg1cXX37NtoHrYXxtNjYArbH
  Price:                 1000000
  Size:                  1
  CreateTime:            2020-07-07 07:00:54.400609 +0000 UTC
  EndTime:               2020-08-06 07:00:54.400609 +0000 UTC
  WithDrawTime:          2020-07-07 07:00:54.400609 +0000 UTC
  UserPay:               1000000upig
```
# 存储业务

## 配置lambda s3 gateway

初始化：

```plain
wget http://download.lambdastorage.com/lambda-storage/0.2.7_rc1/lambda-storage-0.2.7_rc1-testnet.tar.gz
mkdir -p ~/LambdaIM && cd ~/LambdaIM
tar zxvf lambda-storage-0.2.7_rc1-testnet.tar.gz && cd lambda-storage-0.2.7_rc1-testnet
./storagecli init
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
## 运行lambda s3 gateway

```plain
./storagecli gateway run --account user1 --broker.extra_order_id 420CFAFEA58BEEA4918CC84EB399381AF7E44EE6 --debug --daemonize --log.file /tmp/gateway.log
```
--account 为购买空间的用户

--broker.extra_order_id 为用户的空间订单的ID

## 使用aws cli接入lambda s3

安装[awscli](https://docs.aws.amazon.com/cli/latest/userguide/installing.html).

配置用于访问s3网关的key：

```plain
$ aws configure
AWS Access Key ID [None]: accesskey
AWS Secret Access Key [None]: secretkey
Default region name [None]:
Default output format [None]:
```
配置multipart的阈值

```shell
aws configure set default.s3.multipart_threshold 512MB
```
#### 创建bucket

```shell
aws s3 --endpoint=http://localhost:9002/ mb s3://awstest
```
#### 上传文件

```plain
aws s3 --endpoint=http://localhost:9002/ cp /path/to/your/file s3://awstest
```
#### 列出bucket内容

```plain
aws s3 --endpoint=http://localhost:9002/ ls s3://awstest
```
#### 下载文件

```plain
aws s3 --endpoint=http://localhost:9002/ cp s3://awstest/your-file /tmp/new-file
```
## 
## 使用python sdk 接入lambda s3

安装boto3

```plain
pip install boto3
```
```python
#!/usr/bin/env python
# coding: utf-8
"""
refer https://docs.min.io/docs/how-to-use-aws-sdk-for-python-with-minio-server.html
"""
import boto3
from botocore.client import Config
from boto3.s3.transfer import TransferConfig
s3 = boto3.resource('s3',
                    endpoint_url='http://localhost:9002',
                    aws_access_key_id='accesskey',
                    aws_secret_access_key='secretkey',
                    config=Config(signature_version='s3v4'),
                    region_name='')
# create bucket
s3.Bucket('awstest').create()
# list bucket
print("buckets:", [bucket.name for bucket in s3.buckets.all()])
# upload file# https://boto3.amazonaws.com/v1/documentation/api/latest/guide/s3.html#multipart-transfers
MB = 2 ** 20
cfg = TransferConfig(multipart_threshold=512*MB)
s3.Bucket('awstest').upload_file('/path/to/your/file','images/your-file', Config=cfg)
# list file
print("objects in bucket: awstest", [obj.key for obj in s3.Bucket('awstest2').objects.filter(Prefix='images/')])
# download file
s3.Bucket('awstest').download_file('images/your-file', '/tmp/newfile')
```
