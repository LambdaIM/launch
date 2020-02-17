

* [1地址、助记词、加密算法相关](#1地址&助记词&加密算法相关)
* [2数据签名相关](#2数据签名相关)
* [3读取余额和用户信息](#3读取余额和用户信息和节点区块信息)
* [4转账业务和交易详情](#4转账业务和交易详情)
* [5各种交易模拟获取gas(post)](#5各种交易模拟获取gas(post))
* [6节点和节点质押业务,合伙人和质押业务](#6节点和节点质押业务&合伙人和质押业务)
* [7提案与投票业务](#7提案与投票业务)
* [8查询奖励和提取奖励](#8查询奖励和提取奖励)
* [9查询节点收益和提取节点收益](#9查询节点收益和提取节点收益)
* [10资产转换](#10资产转换)


业务发送说明：
发送数据可以采用同步或异步方式，同步方式可以获取因为格式等造成的错误信息    
异步为async  
同步为 block

主网的钱包服务地址：39.107.247.86:13659

测试网的钱包服务地址：47.93.196.236:13659



# 1地址&助记词&加密算法相关
生成助记词 使用 bip39   钱包和链使用长度为256 的24个单词

生成hd钱包 使用bip32  derivePath 为  '44\'/364\'/0\'/0/0'

钱包生成的地址和链生成的地址保持一致 需要使用相同的 derivePath

例如

```
const bip39 = require('bip39');
const bip32 = require('bip32');
const crypto = require('crypto');
const secp256k1 = require('secp256k1');


exports.generateRandomMnemonic = function(strength) {
  return bip39.generateMnemonic(strength);
};
/**
 * Get keys (private/public) from mnemonic and path (bip32/39/44).
 *
 * @param  {String} mnemonic        Mnemonic words.
 * @param  {String} path            BIP44 path.
 * @return {Object.<Buffer,Buffer>} Wallet object contains privateKey/publicKey.
 */
exports.getKeysFromMnemonic = function getKeysFromMnemonic(mnemonic, path = '44\'/364\'/0\'/0/0') {
  const seed = bip39.mnemonicToSeedSync(mnemonic);
  const master = bip32.fromSeed(seed);
  const wallet = master.derivePath(path);


  return wallet;
};
```



生成地址对生成的公钥 进行sha256 加密后，  
再用Ripemd160 处理   
再用bech32 添加 lambda 前缀  
例如

```
const bech32 = require('bech32');
const Ripemd160 = require('ripemd160');
const crypto = require('crypto');


/**
 * @const lambda bech32 address prefix.
 *
 * @type    {String}
 * @default
 */
const PREFIX = 'lambda';
const PREFIXDev = 'lambdavaloper';


/**
 * Get lambda  address (bech32) from public key.
 *
 * @param  {Buffer} publicKey Public key
 * @return {String}           Bech32 address
 */
exports.getAddress = function getAddress(publicKey) {
  const hash = crypto.createHash('sha256')
    .update(publicKey)
    .digest();


  const address = new Ripemd160().update(hash).digest();
  const words = bech32.toWords(address);


  return bech32.encode(PREFIX, words);
};
```
# 2数据签名相关
首先对需要签名的数据进行sha256 计算 ，再对 计算结果和私钥 用 secp256k1 进行签名

例如

```
const bip39 = require('bip39');
const bip32 = require('bip32');
const crypto = require('crypto');
const secp256k1 = require('secp256k1');
function sign(bytes, privateKey) {
  const hash = crypto.createHash('sha256')
    .update(bytes)
    .digest();
  return secp256k1.sign(hash, privateKey).signature;
}
```

# 3读取余额和用户信息和节点区块信息
## 账户信息
### 账户信息
```
 /auth/accounts/${address}
```
 返回结果例子   
 包含账号各种代币的余额，后6位用于表示小数
例如1lamb=1000000ulamb  

其中sequenc 用于下次发送交易时候用

```
{
  "type": "auth/Account",
  "value": {
    "address": "lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt",
    "coins": [
      {
        "denom": "ulamb", 代币的名称
        "amount": "10848193224664"  代币的数量
      },
      {
        "denom": "utbb",
        "amount": "10031000004"
      },
      {
        "denom": "ufeiniao",
        "amount": "10031000004"
      }
    ],
    "public_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "AjmQ01Z+IoHuKLdPaFzV6IJQB88ahW2qv2rEw2H4B5dq"
    },
    "account_number": "1",
    "sequence": "114"   
  }
}
```
## 节点区块信息接口
### 获取最新的区块信息 接口  
`/blocks/latest`
### 获取链接的节点的 节点信息接口  
`/node_info`
```
{
  "protocol_version": {
    "p2p": "7",
    "block": "10",
    "app": "0"
  },
  "id": "e02882af5bdafa5aec086c32b8398c268d2337f1",
  "listen_addr": "tcp://0.0.0.0:26656",
  "network": "lambda-chain-test4.0",  链的版本号
  "version": "0.31.5",
  "channels": "4020212223303800",
  "moniker": "cv-moniker-1",  链接的验证节点的名称
  "other": {
    "tx_index": "on",
    "rpc_address": "tcp://0.0.0.0:26657"
  }
}
```
### 获取链同步信息的接口     
`/syncing`
### 获取全网代币名称   
`/asset/all`
```
[
  {
    "address": "lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr",
    "asset": {
      "denom": "ubtc",   //代币的名称
      "amount": "100000000"
    },
    "Token": {
      "denom": "ulamb",
      "amount": "1000000000000"
    },
    "name": "BTC Coin",
    "mintable": false,
    "curr_supply": {
      "denom": "ubtc",
      "amount": "100000000"
    },
    "lock_supply": {
      "denom": "ubtc",
      "amount": "0"
    }
  },
  {
    "address": "lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr",
    "asset": {
      "denom": "uhpt",
      "amount": "9999999999"
    },
    "Token": {
      "denom": "ulamb",
      "amount": "1000000000000"
    },
    "name": "HPT Coin",
    "mintable": false,
    "curr_supply": {
      "denom": "uhpt",
      "amount": "9999999999"
    },
    "lock_supply": {
      "denom": "uhpt",
      "amount": "0"
    }
  },
  {
    "address": "lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr",
    "asset": {
      "denom": "uxxb",
      "amount": "100000000"
    },
    "Token": {
      "denom": "ulamb",
      "amount": "1000000000000"
    },
    "name": "XXB Coin",
    "mintable": true,
    "curr_supply": {
      "denom": "uxxb",
      "amount": "100000000"
    },
    "lock_supply": {
      "denom": "uxxb",
      "amount": "0"
    }
  }
]
```



# 4转账业务和交易详情
 发送接口

```
`${cosmosRESTURL}/txs`   
类型 post  
数据类型json
```
模拟接口获取gas

```
/bank/accounts/${senderAddress}/transfers
类型 post
数据类型 json
```
 用于进行签名的数据结构

```
{
  "account_number": "1",  //通过用户信息获取
  "chain_id": "lambda-chain-test2.5", //链的版本号 通过最新的区块信息获取 
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
  "sequence": "125"  //通过获取用户信息接口获取
}
```
 用于发送数据的的数据结构

```
{
  "tx": {
    "msg": [{
      "type": "cosmos-sdk/MsgSend",
      "value": {
        "amount": [{
          "amount": "1000000",
          "denom": "ulamb"
        }],
        "from_address": "lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt",
        "to_address": "lambda1hynqrp2f80jqs86gu8nd5wwcnek2wwd3esszg0"
      }
    }],
    "fee": {
      "amount": [{
        "amount": "101745",
        "denom": "ulamb"
      }],
      "gas": "40698"
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
  "mode": "async"    发送交易的方式async 为异步，block 为同步
}
```
 获取和转账相关的交易记录
```
/txs?sender=${addr}&page=1000000            获取最新发送的交易
/txs?recipient=${addr}&page=1000000         获取最新接受的交易
```
根据交易哈希获取交易详情
```
`/txs/${hash}`
```

# 5各种交易模拟获取gas(post)
钱包里面默认的gas的价格为 2.5e-6

交易的费用为 gas * gas的价格

接口

    'cosmos-sdk/MsgSend': () => `/bank/accounts/${senderAddress}/transfers`,

    'lambda/MsgDelegate': () => `/staking/delegators/${senderAddress}/delegations`,

    'lambda/MsgUndelegate': () => `/staking/delegators/${senderAddress}/unbonding_delegations`,

    'lambda/MsgBeginRedelegate': () => `/staking/delegators/${senderAddress}/redelegations`,

    'cosmos-sdk/MsgSubmitProposal': () => `/gov/proposals`,

    'cosmos-sdk/MsgVote': () => `/gov/proposals/${msg.value.proposal_id}/votes`,

    'cosmos-sdk/MsgDeposit': () => `/gov/proposals/${msg.value.proposal_id}/deposits`,

    'cosmos-sdk/MsgWithdrawDelegationReward': () => `/distribution/delegators/${senderAddress}/rewards`,

    'lambda/MsgAssetPledge': () => `/asset/pledge`,

    'lambda/MsgAssetDrop': () => `/asset/drop`,

    'cosmos-sdk/MsgWithdrawValidatorCommission': () => `/distribution/delegators/${senderAddress}/rewards`,

    'lambda/MsgCreateSellOrder': () => `/market/create-sellorder`,

    'lambda/MsgCreateBuyOrder': () => `/market/create-buyorder`,

    'lambda/MsgCreateMiner': () => `/market/create-miner`,

    'lambda/MsgCreateMachine': () => `/market/create-machine`

js 里面数据的拼接方式

```
function createRESTPOSTObject (senderAddress, chainId, { sequence, accountNumber, memo }, msg) {
  const requestMetaData = {
    sequence,
    from: senderAddress,
    account_number: accountNumber,
    chain_id: chainId,
    simulate: true,
    memo
  }


  return { base_req: requestMetaData, ...msg.value }
```
}


【转账交易的例子 post 的内容】
```
{
  "base_req": {
    "sequence": "208",
    "from": "lambda163q4m634nq8les4nuvdvz49tk6ae**********",
    "account_number": "6",
    "chain_id": "lambda-chain-test4.0",
    "simulate": true,
    "memo": ""
  },
  "amount": [{
    "amount": "1000000",
    "denom": "ulamb"
  }],
  "from_address": "lambda163q4m634nq8les4nuvdvz49tk6ae**********",
  "to_address": "lambda16cheh6j34ncyunwgfkq2940cs8222jka0fsp4k"
}
```
返回结果 
```
  {"gas_estimate":"28077"}
```





# 6节点和节点质押业务&合伙人和质押业务
质押使用的代币为tbb

读取节点列表

```
/staking/validators?status=unbonding   //禁闭中
/staking/validators?status=bonded      //质押中
/staking/validators?status=unbonded     //未解禁
```
unbonding是反质押中，或被禁闭中  
unbonded是反质押完成 或 被禁的节点过了21天还没解禁

返回结果举例

```
[
 {
    "operator_address": "lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl", //验证节点的操作地址
    "consensus_pubkey": "lambdavalconspub1zcjduepqp7ccjeshlpslrzjj75je5kn6dhtq8l5nnl6h5jtavgsf5tyekfsqe4mnh9",
    "jailed": false,   是否正在禁闭
    "status": 2, //状态2表示正常
    "tokens": "1313966657",  //这个节点一共质押了多少tbb代币
    "delegator_shares": "1313966657.000000000000000000",
    "description": {  //节点介绍信息
      "moniker": "cv-moniker-2",//节点名称
      "identity": "",
      "website": "",//网址
      "details": ""//简介
    },
    "unbonding_height": "0",
    "unbonding_time": "2019-09-14T06:15:39.017728976Z",
    "commission": {  //节点收益
      "rate": "0.250000000000000000",  //收益百分比
      "max_rate": "0.250000000000000000", //最大收益
      "max_change_rate": "0.010000000000000000", //收益变化
      "update_time": "2019-08-27T02:48:18.857634087Z"
    },
    "min_self_delegation": "666666666"   //节点自己给自己质押了多少tbb代币
  }
]
```
## 质押相关接口
### 查询个人质押信息的接口
`/staking/delegators/${addr}/delegations`
```
[
  {
    "delegator_address": "lambda163q4m634nq8les4nuvdvz49tk6ae**********",  //质押人的地址
    "validator_address": "lambdavaloper1zyqnx5efrdh0nvv8wtc6f7kasm02jxw7rkva9v",  //节点的操作地址
    "shares": "100000.000000000000000000"   //质押占的分数
  },
  {
    "delegator_address": "lambda163q4m634nq8les4nuvdvz49tk6ae**********",
    "validator_address": "lambdavaloper17tnjj0r02eupk8rsd23aq2x0cn7pkjdf6tezda",
    "shares": "800000.000000000000000000"
  }
]
```

### 个人解除质押列表接口 
验证节点的取消质押列表

`/staking/delegators/${addr}/unbonding_delegations`

合伙人的取消质押列表 

`/staking/delegators/${addr}/unbonding_partner_delegations`

### 获取用户在一个节点下质押的奖励
`/distribution/delegators/${delegatorAddr}/rewards/${validatorAddr}`

例如   [http://47.93.196.236:13659/distribution/delegators/lambda163q4m634nq8les4nuvdvz49tk6aeh926t0ccsc/rewards/lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl](http://47.93.196.236:13659/distribution/delegators/lambda163q4m634nq8les4nuvdvz49tk6aeh926t0ccsc/rewards/lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl)

```
[
  {
    "denom": "ulamb",
    "amount": "3514296927.123515563816500000"
  }
]
```
### 查询某个节点的详情
`/staking/validators/${addr}`


### 获取质押相关参数的接口 
`/staking/parameters`
```
{
  "unbonding_time": "259200000000000",  //解除质押需要的时间
  "max_validators": 100,  //最大验证节点数量
  "max_entries": 7,
  "bond_denom": "utbb",  质押用到的代币
  "supply_denom": "ulamb",
  "consensus_validator_min_self_delegation": "666666666",
  "partner_validator_min_self_delegation": "33333333",
  "consensus_validator_min_delegation": "1000000",
  "partner_validator_min_delegation": "100000",
  "consensus_validator_fixed_commission_rate": "0.250000000000000000",
  "partner_validator_fixed_commission_rate": "0.250000000000000000"
}
```

### shares 和tbb转换【个人质押量计算】
个人质押后获取到质押分份额后，显示如果是显示质押的tbb数量需要进行转换计算

shares*(tokens/delegator_shares)

用个人的shares 除以节点总的shares 再乘以节点总的tokens


读取节点详情

```
/staking/validators/${addr}
```
返回结果
```
{
  "operator_address": "lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl",
  "consensus_pubkey": "lambdavalconspub1zcjduepqp7ccjeshlpslrzjj75je5kn6dhtq8l5nnl6h5jtavgsf5tyekfsqe4mnh9",
  "jailed": false,
  "status": 2,
  "tokens": "1313966657",
  "delegator_shares": "1313966657.000000000000000000",
  "description": {
    "moniker": "cv-moniker-2",
    "identity": "",
    "website": "",
    "details": ""
  },
  "unbonding_height": "0",
  "unbonding_time": "2019-09-14T06:15:39.017728976Z",
  "commission": {
    "rate": "0.250000000000000000",
    "max_rate": "0.250000000000000000",
    "max_change_rate": "0.010000000000000000",
    "update_time": "2019-08-27T02:48:18.857634087Z"
  },
  "min_self_delegation": "666666666"
}
```


### 质押模拟接口【详细信息见获取gas部分】

```
/staking/delegators/${senderAddress}/delegations
```
### 质押接口和质押的数据结构
质押接口同交易接口


签名数据的结构

```
{
  "account_number": "1",
  "chain_id": "lambda-chain-test2.5",
  "fee": {
    "amount": [{
      "amount": "421935",
      "denom": "ulamb"
    }],
    "gas": "168774"
  },
  "memo": "",
  "msgs": [{
    "type": "lambda/MsgDelegate",
    "value": {
      "amount": {
        "amount": "1000000",  //质押的数量
        "denom": "utbb"  //质押的代币类型
      },
      "delegator_address": "lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt",    质押人的地址
      "validator_address": "lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl",  //验证节点的操作地址
      "validator_type": 1    类型1 表示验证节点 0表示合伙人
    }
  }],
  "sequence": "126"
}
```
发送数据的结构
```
{
  "tx": {
    "msg": [{
      "type": "lambda/MsgDelegate",
      "value": {
        "amount": {
          "amount": "1000000",
          "denom": "utbb"
        },
        "delegator_address": "lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt",
        "validator_address": "lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl",
        "validator_type": 1
      }
    }],
    "fee": {
      "amount": [{
        "amount": "421935",
        "denom": "ulamb"
      }],
      "gas": "168774"
    },
    "signatures": [{
      "signature": "xKJeVWVPH+NrOd+NogBesdYUSM3a8PJ/MiUxHvVpQDpok6WZ4yd0SHTc0/choPvT81tXHFhg9Lrp/tSTr3sFOA==",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "AjmQ01Z+IoHuKLdPaFzV6IJQB88ahW2qv2rEw2H4B5dq"
      }
    }],
    "memo": ""
  },
  "mode": "async"
}
```


### 转质押接口和数据结构
接口同交易接口

转质押的签名数据结构

```
{
  "account_number": "6",
  "chain_id": "lambda-chain-test4.0",
  "fee": {
    "amount": [{
      "amount": "575325",
      "denom": "ulamb"
    }],
    "gas": "230130"
  },
  "memo": "",
  "msgs": [{
    "type": "lambda/MsgBeginRedelegate",
    "value": {
      "amount": {
        "amount": "1000000",  转质押的数量
        "denom": "utbb"
      },
      "delegator_address": "lambda163q4m634nq8les4nuvdvz49tk6ae**********",  质押人的地址
      "validator_dst_address": "lambdavaloper1r340rrv9fs95gqy5087e2mtz82vvwrglt6amx3", 新的质押地址
      "validator_src_address": "lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl",  旧的质押地址
      "validator_type": 1  节点类型  验证节点为1 合伙人为0
    }
  }],
  "sequence": "208"
}
```
转质押发送数据的结构

```
{
  "tx": {
    "msg": [{
      "type": "lambda/MsgBeginRedelegate",
      "value": {
        "amount": {
          "amount": "1000000",
          "denom": "utbb"
        },
        "delegator_address": "lambda163q4m634nq8les4nuvdvz49tk6ae**********",
        "validator_dst_address": "lambdavaloper1r340rrv9fs95gqy5087e2mtz82vvwrglt6amx3",
        "validator_src_address": "lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl",
        "validator_type": 1
      }
    }],
    "fee": {
      "amount": [{
        "amount": "575325",
        "denom": "ulamb"
      }],
      "gas": "230130"
    },
    "signatures": [{
      "signature": "5Ejsk1J1bwBU9eJWsquhKOq5tW081W7CumAGbfaf3dguWm4cVE/wb29zzb0VLYNErx2jo6Ky9TQfs3Ib7uXy7g==",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "A8XABxcKi0bX6P/K7CaifPJvfk/pSrf4E7mBM7yV89ZR"
      }
    }],
    "memo": ""
  },
  "mode": "block"
}
```
### 取消质押接口和数据结构
接口同交易接口

签名的数据结构

```
{
  "account_number": "6",
  "chain_id": "lambda-chain-test4.0",
  "fee": {
    "amount": [{
      "amount": "404805",
      "denom": "ulamb"
    }],
    "gas": "161922"
  },
  "memo": "",
  "msgs": [{
    "type": "lambda/MsgUndelegate",
    "value": {
      "amount": {
        "amount": "1000000",//取消质押的数量
        "denom": "utbb"
      },
      "delegator_address": "lambda163q4m634nq8les4nuvdvz49tk6ae**********",//操作人的地址
      "validator_address": "lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl",//节点的操作地址
      "validator_type": 1  节点类型 验证节点为1 合伙人为0
    }
  }],
  "sequence": "209"
}
```
发送数据的的数据结构
```
{
  "tx": {
    "msg": [{
      "type": "lambda/MsgUndelegate",
      "value": {
        "amount": {
          "amount": "1000000",  
          "denom": "utbb"
        },
        "delegator_address": "lambda163q4m634nq8les4nuvdvz49tk6ae**********",  
        "validator_address": "lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl",  
        "validator_type": 1    
      }
    }],
    "fee": {
      "amount": [{
        "amount": "404805",
        "denom": "ulamb"
      }],
      "gas": "161922"
    },
    "signatures": [{
      "signature": "dwmnrm6iAQzOv2GfpyzQYcY0zyfqMnCKzPFhSkvGjx5hyEbNYcWKRknahF1X6N1zciGx4ClhuhpXbau96rfsvQ==",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "A8XABxcKi0bX6P/K7CaifPJvfk/pSrf4E7mBM7yV89ZR"
      }
    }],
    "memo": ""
  },
  "mode": "block"
}
```


## 合伙人相关接口

获取合伙人列表

```
/staking/partner_validators?status=unbonding
/staking/partner_validators?status=bonded
/staking/partner_validators?status=unbonded
```
获取合伙人详情
```
/staking/partner_validators/${addr}
```
质押到合伙人与质押到节点数据结构一致 传入的validator_type 为0即可


# 7提案与投票业务
## 提案接口
### 提案列表
接口 `/gov/proposals`

返回结果

```
[{
  "content": {
    "type": "cosmos-sdk/TextProposal",  //提案的类型
    "value": {
      "title": "文本提案中文换行测试",    //标题
      "description": "诺贝尔化学奖揭晓。"  //提案内容
    }
  },
  "id": "1",  //提案id
  "proposal_status": "Rejected",  提案状态
  "final_tally_result": {
    "yes": "90000",  同意的票数
    "abstain": "16190009", 弃权的票数
    "no": "0",反对的票数
    "no_with_veto": "0" 强烈反对的票数
  },
  "submit_time": "2019-10-10T07:21:22.988264879Z", 提交时间
  "deposit_end_time": "2019-10-12T07:21:22.988264879Z",存款结束的时间
  "total_deposit": [{    存钱的数量
    "denom": "ulamb",
    "amount": "11023000000"
  }],
  "voting_start_time": "2019-10-11T03:48:59.199943178Z",  投票开始时间 
  "voting_end_time": "2019-10-13T03:48:59.199943178Z" 投票结束的时间
}]
```

### 提案详情
接口 `/gov/proposals/${proposalId}`

返回结果

```
{
  "content": {
    "type": "cosmos-sdk/TextProposal",
    "value": {
      "title": "Test Proposal",         
      "description": "This is for test"
    }
  },
  "id": "7",
  "proposal_status": "Rejected",
  "final_tally_result": {
    "yes": "10000000",
    "abstain": "0",
    "no": "0",
    "no_with_veto": "0"
  },
  "submit_time": "2019-11-27T07:04:13.857176797Z",
  "deposit_end_time": "2019-11-29T07:04:13.857176797Z",
  "total_deposit": [
    {
      "denom": "ulamb",
      "amount": "10000000000"
    }
  ],
  "voting_start_time": "2019-11-27T07:42:40.78653812Z",
  "voting_end_time": "2019-11-29T07:42:40.78653812Z"
}
```
### 不同提案类型 对应不同的数据结构
ParameterChangeProposal   参数变更

```
changes: [{
 key: "MaxValidators"
 subspace: "staking"
 value: "105" 
}]
description: "2"
title: "1"
```
CommunityPoolSpendProposal 社区基金
```
amount: null
description: "2"
recipient: "lambda1hynqrp2f80jqs86gu8nd5wwcnek2wwd3esszg0"
title: "1"
```
BurnCoinsProposal  销毁币
```
burn_amount: null
description: "2"
title: "1"
```
TextProposal 文本
```
description: "2"
title: "1"
```
SoftwareUpgradeProposal  软件升级
```
```




### 存入押金
接口同交易接口

数据结构

```
{
  "account_number": "6",
  "chain_id": "lambda-chain-test4.0",
  "fee": {
    "amount": [{
      "amount": "139088",
      "denom": "ulamb"
    }],
    "gas": "55635"
  },
  "memo": "",
  "msgs": [{
    "type": "cosmos-sdk/MsgDeposit",
    "value": {
      "amount": [{
        "amount": "1000000",   存入押金的金额
        "denom": "ulamb"
      }],
      "depositor": "lambda163q4m634nq8les4nuvdvz49tk6ae**********", 操作人的地址
      "proposal_id": "9" 提案的编号
    }
  }],
  "sequence": "211"
}
```
发送数据的结构

```
{
  "tx": {
    "msg": [{
      "type": "cosmos-sdk/MsgDeposit",
      "value": {
        "amount": [{
          "amount": "1000000",
          "denom": "ulamb"
        }],
        "depositor": "lambda163q4m634nq8les4nuvdvz49tk6ae**********",
        "proposal_id": "9"
      }
    }],
    "fee": {
      "amount": [{
        "amount": "139088",
        "denom": "ulamb"
      }],
      "gas": "55635"
    },
    "signatures": [{
      "signature": "95hKC9qtiOripRmG2EnOW63mtnQf5TbLS/XlfZ+PuI5q8ogeGgmqgq0YIBUOCQDvxHgovCBGZZhJKEqxgC0ehQ==",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "A8XABxcKi0bX6P/K7CaifPJvfk/pSrf4E7mBM7yV89ZR"
      }
    }],
    "memo": ""
  },
  "mode": "block"
}
```

### 投票
接口同交易接口

签名数据结构

```
{
  "account_number": "6",
  "chain_id": "lambda-chain-test4.0",
  "fee": {
    "amount": [{
      "amount": "52200",
      "denom": "ulamb"
    }],
    "gas": "20880"
  },
  "memo": "",
  "msgs": [{
    "type": "cosmos-sdk/MsgVote",
    "value": {
      "option": "Yes",  投票的选项
      "proposal_id": "9", 提案id
      "voter": "lambda163q4m634nq8les4nuvdvz49tk6ae**********" 投票人地址
    }
  }],
  "sequence": "214"
}
```
发送数据的数据结构

```
{
  "tx": {
    "msg": [{
      "type": "cosmos-sdk/MsgVote",
      "value": {
        "option": "Yes",  
        "proposal_id": "9",  
        "voter": "lambda163q4m634nq8les4nuvdvz49tk6ae**********"  
      }
    }],
    "fee": {
      "amount": [{
        "amount": "52200",
        "denom": "ulamb"
      }],
      "gas": "20880"
    },
    "signatures": [{
      "signature": "KPi3MwnMijT/u0qmm5x2qLTFJEmi0Tn6/jxJRSMzkL8p18oe2WmDlwLcHMoEpqpnuPND/Vt0/UIagROWX0hgoQ==",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "A8XABxcKi0bX6P/K7CaifPJvfk/pSrf4E7mBM7yV89ZR"
      }
    }],
    "memo": ""
  },
  "mode": "block"
}
```
## 提案查询接口
### 获取我的存钱
`/gov/proposals/${proposalId}/deposits/${address}`

```
{
  "proposal_id": "9",
  "depositor": "lambda163q4m634nq8les4nuvdvz49tk6ae**********", //操作人的地址
  "amount": [{
    "denom": "ulamb",
    "amount": "10002000000"   存入的进入
  }]
}
```
### 获取我的投票
`/gov/proposals/${proposalId}/votes/${address}`

```
{
  "proposal_id": "9", 
  "voter": "lambda163q4m634nq8les4nuvdvz49tk6ae**********",
  "option": "Yes" 我投的票
}
```


### 获取提案的投票结果
`/gov/proposals/${proposalId}/tally`

```
{
  "yes": "13590009",
  "abstain": "0",
  "no": "0",
  "no_with_veto": "0"
}
```


### 获取提案公共参数 
/gov/parameters/deposit

```
{
  "min_deposit": [{  进入投票需要存多少钱
    "denom": "ulamb",
    "amount": "10000000000"
  }],
  "max_deposit_period": "172800000000000"  存钱的时段
}
```
`/staking/pool`
```
{
  "not_bonded_tokens": "999386446677",
  "bonded_tokens": "2817286659" 质押的代币量 这个值用以计算投票量占全网总量的多少
}
```

# 8查询奖励和提取奖励

查询当前账户的奖励 总数  

/distribution/delegators/${delegatorAddr}/rewards

```
[
  {
    "denom": "ulamb",
    "amount": "103272443719.555139184730000000"
  }
]
```
查询在节点质押的奖励 --看在哪些节点下质押了

```
/staking/delegators/${addr}/delegations
```
查询在合伙人质押的奖励---看在哪些合伙人下质押了
```
/staking/delegators/${addr}/partner_delegations
```
提取奖励   提取奖励不需要传入数值，只需要传入 节点地址和质押人地址即可

发送交易的接口同交易接口

签名的数据结构

```
{
  "account_number": "1",
  "chain_id": "lambda-chain-test2.5",
  "fee": {
    "amount": [{
      "amount": "635848",
      "denom": "ulamb"
    }],
    "gas": "254339"
  },
  "memo": "",
  "msgs": [{
    "type": "cosmos-sdk/MsgWithdrawDelegationReward",
    "value": {
      "delegator_address": "lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt",  //质押人地址
      "validator_address": "lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl" //节点地址  
    }
  }, {
    "type": "cosmos-sdk/MsgWithdrawDelegationReward",
    "value": {
      "delegator_address": "lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt",
      "validator_address": "lambdavaloper1r340rrv9fs95gqy5087e2mtz82vvwrglt6amx3"
    }
  }, {
    "type": "cosmos-sdk/MsgWithdrawDelegationReward",
    "value": {
      "delegator_address": "lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt",
      "validator_address": "lambdavaloper1thj5fv8d0dsh3aealhpxm9mvgxjfh87suwuj2h"
    }
  }],
  "sequence": "127"
}
```
发送交易的数据结构
```
{
  "tx": {
    "msg": [{
      "type": "cosmos-sdk/MsgWithdrawDelegationReward",
      "value": {
        "delegator_address": "lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt",
        "validator_address": "lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl"
      }
    }, {
      "type": "cosmos-sdk/MsgWithdrawDelegationReward",
      "value": {
        "delegator_address": "lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt",
        "validator_address": "lambdavaloper1r340rrv9fs95gqy5087e2mtz82vvwrglt6amx3"
      }
    }, {
      "type": "cosmos-sdk/MsgWithdrawDelegationReward",
      "value": {
        "delegator_address": "lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt",
        "validator_address": "lambdavaloper1thj5fv8d0dsh3aealhpxm9mvgxjfh87suwuj2h"
      }
    }],
    "fee": {
      "amount": [{
        "amount": "635848",
        "denom": "ulamb"
      }],
      "gas": "254339"
    },
    "signatures": [{
      "signature": "CNxU2hyIL1Az8Mb+Btt3APP1f476Q+Z/bTzmpsTQV2l3Od5TLfTlgS4hJkhLsCHlzXbCCJlhDz9d2OK3IvupCQ==",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "AjmQ01Z+IoHuKLdPaFzV6IJQB88ahW2qv2rEw2H4B5dq"
      }
    }],
    "memo": ""
  },
  "mode": "async"
}
```
# 9查询节点收益和提取节点收益
这里传的地址为节点操作地址 例如

validatorAddr 为 节点的操作地址     

```
`/distribution/validators/${validatorAddr}`
```
例如 [http://47.93.196.236:13659/distribution/validators/lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl](http://47.93.196.236:13659/distribution/validators/lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl)

返回结果

```
{
  "operator_address": "lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt",
  "self_bond_rewards": [{  //自己质押的收益
    "denom": "ulamb",
    "amount": "1318824629026.957070122504282575"
  }],
  "val_commission": [{    //收取矿工的佣金
    "denom": "ulamb",
    "amount": "827774754064.482428092893265856"
  }]
}
```
提取节点收益
签名数据格式

```
{
  "account_number": "1",
  "chain_id": "lambda-chain-test2.5",
  "fee": {
    "amount": [{
      "amount": "636128",
      "denom": "ulamb"
    }],
    "gas": "254451"
  },
  "memo": "",
  "msgs": [{
    "type": "cosmos-sdk/MsgWithdrawValidatorCommission",
    "value": {
      "validator_address": "lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl"   //节点的操作地址 
    }
  }],
  "sequence": "128"
}
```
发送数据格式
```
{
  "tx": {
    "msg": [{
      "type": "cosmos-sdk/MsgWithdrawValidatorCommission",
      "value": {
        "validator_address": "lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl"
      }
    }],
    "fee": {
      "amount": [{
        "amount": "636128",
        "denom": "ulamb"
      }],
      "gas": "254451"
    },
    "signatures": [{
      "signature": "iCa63qOUVNsxIsynOuPtrZRtqWYz5IWGz624Vzn2nBhOEadmsLm87Ms4U2W/V6o74e+6OmkKIERkFFJngU7ABw==",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "AjmQ01Z+IoHuKLdPaFzV6IJQB88ahW2qv2rEw2H4B5dq"
      }
    }],
    "memo": ""
  },
  "mode": "async"
}
```

# 10资产转换
规则 3000个lamb 兑换1个tbb 且必须是整数

接口同交易接口

### lamb转tbb
签名前的数据

```
{
  "account_number": "6",
  "chain_id": "lambda-chain-test4.0",
  "fee": {
    "amount": [{
      "amount": "140798",
      "denom": "ulamb"
    }],
    "gas": "56319"
  },
  "memo": "",
  "msgs": [{
    "type": "lambda/MsgAssetPledge",  交易的类型
    "value": {
      "address": "lambda163q4m634nq8les4nuvdvz49tk6aeh926t0ccsc", 发送人地址
      "asset": {
        "amount": "1000000",
        "denom": "utbb"
      },
      "token": {
        "amount": "3000000000",    lamb的数量
        "denom": "ulamb"
      }
    }
  }],
  "sequence": "216"
}
```
发送的数据
```
{
  "tx": {
    "msg": [{
      "type": "lambda/MsgAssetPledge",
      "value": {
        "address": "lambda163q4m634nq8les4nuvdvz49tk6aeh926t0ccsc",
        "asset": {
          "amount": "1000000",
          "denom": "utbb"
        },
        "token": {
          "amount": "3000000000",
          "denom": "ulamb"
        }
      }
    }],
    "fee": {
      "amount": [{
        "amount": "140798",
        "denom": "ulamb"
      }],
      "gas": "56319"
    },
    "signatures": [{
      "signature": "0lmFd0cpyBTxWpgkvOUT7VfPIr7UY0sD8mlQEneJaA1upRlP9H/caHYA6Fikp0+un/GxeBRahXKuFvrsEFuXuQ==",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "A8XABxcKi0bX6P/K7CaifPJvfk/pSrf4E7mBM7yV89ZR"
      }
    }],
    "memo": ""
  },
  "mode": "block"
}
```
### tbb转lamb
签名前的数据

```
{
  "account_number": "6",
  "chain_id": "lambda-chain-test4.0",
  "fee": {
    "amount": [{
      "amount": "140798",
      "denom": "ulamb"
    }],
    "gas": "56319"
  },
  "memo": "",
  "msgs": [{
    "type": "lambda/MsgAssetDrop",  交易类型
    "value": {
      "address": "lambda163q4m634nq8les4nuvdvz49tk6aeh926t0ccsc",  发送人的地址
      "asset": {
        "amount": "1000000",  tbb的数量
        "denom": "utbb"
      },
      "token": {
        "amount": "3000000000", lamb的数量
        "denom": "ulamb"
      }
    }
  }],
  "sequence": "217"
}
```
发送的数据
```
{
  "tx": {
    "msg": [{
      "type": "lambda/MsgAssetDrop",
      "value": {
        "address": "lambda163q4m634nq8les4nuvdvz49tk6aeh926t0ccsc",
        "asset": {
          "amount": "1000000",
          "denom": "utbb"
        },
        "token": {
          "amount": "3000000000",
          "denom": "ulamb"
        }
      }
    }],
    "fee": {
      "amount": [{
        "amount": "140798",
        "denom": "ulamb"
      }],
      "gas": "56319"
    },
    "signatures": [{
      "signature": "6tKf/brt/llh4XgiwBS65aDMvt7cV13pQBN2ph/nJdcB44dPxlQ0LGopZ76un+AH+RJYa/NCPtDTW4M7viPaoA==",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "A8XABxcKi0bX6P/K7CaifPJvfk/pSrf4E7mBM7yV89ZR"
      }
    }],
    "memo": ""
  },
  "mode": "block"
}
```

