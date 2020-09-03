# 交易所对接

```
主网的地址： 39.107.247.86:13659

测试网的地址： bj1.testnet.lambdastorage.com:13659
```

## 一、地址生成算法

生成助记词 使用 bip39   钱包和区块链使用长度为256位的助记词（24个单词）

生成公钥私钥对 使用bip32  derivePath 为  '44\'/364\'/0\'/0/0'

钱包生成的地址和链生成的地址保持一致 需要使用相同的 derivePath

代码举例 https://github.com/LambdaIM/walletdoccode/blob/master/lib/crypto.js


根据公钥生成地址

生成地址对生成的公钥 进行sha256 加密后，在用Ripemd160 处理， 再用bech32 添加 lambda 对应的前缀

例如  lambda 地址前缀 为lambda：`lambda1z4hs23xwjuudm44nhgcde0zxf5y63su8deuqs3`

代码举例 
https://github.com/LambdaIM/walletdoccode/blob/master/lib/address.js


## 二、查询地址余额[GET]

  接口 http://URL/bank/balances/{address}


  例如 http://bj1.testnet.lambdastorage.com:13659/bank/balances/lambda1y8zw42uahus0mn8064mmkfyy8uhcjjjalc0vzl
  
  返回结果 举例
  ```
 [{
	"denom": "ulamb",
	"amount": "1606999722941"
}, {
	"denom": "utbb",
	"amount": "201000000"
}]
  ```
## 三、查询地址nonce[GET]

接口 http://URL/auth/accounts/{address}

例如 http://bj1.testnet.lambdastorage.com:13659/auth/accounts/lambda1y8zw42uahus0mn8064mmkfyy8uhcjjjalc0vzl

返回结果 举例
```
{
	"type": "auth/Account",
	"value": {
		"address": "lambda1y8zw42uahus0mn8064mmkfyy8uhcjjjalc0vzl",
		"coins": [{
			"denom": "ulamb",
			"amount": "1606999722941"
		}, {
			"denom": "utbb",
			"amount": "201000000"
		}],
		"public_key": {
			"type": "tendermint/PubKeySecp256k1",
			"value": "AlOZyAXmfqpXzAwPQfU8aGhwXudIdNNv2FQ5jGHRHWEL"
		},
		"account_number": "21", //账户编号 发送交易用
		"sequence": "3" //sequence 发送交易用
	} 
}
```
## 四、转帐 [POST]
接口 http://URL/txs

发送交易分为三个部分

### 1 拼接交易的数据结构用于签名
不同的交易类型，msgs数组中的对象的结构会有差别
```
{
    "account_number": "1",  //通过用户信息获取
    "chain_id": "lambda-chain-test2.5", //链的版本号 通过最新的区块信息获取 
    "fee": {//手续费
        "amount": [{
            "amount": "101745",gas的价格 
            "denom": "ulamb" 
        }],
        "gas": "40698"  // gas 
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
手续费部分gas 可以填的大一点例如2000000，amount 表示gas的价格可以填的小一点例如1(表示1ulamb)

每次发起交易前，均要通过账户信息接口获取最新的sequence、account_number

http://bj1.testnet.lambdastorage.com:13659/auth/accounts/lambda1prrcl9674j4aqrgrzmys5e28lkcxmntx2gm2zt

chain_id 通过node_info 接口获取
http://bj1.testnet.lambdastorage.com:13659/node_info

### 2 对拼接好的数据结构进行签名
数据签名相关代码举例 https://github.com/LambdaIM/walletdoccode/blob/master/lib/crypto.js

例如 对第1步数据结构签名，结果转为base64格式
```
fa9bUlNRA3qa9PEYR2py6CgpQbbqVsuKhJRowMdlf90byj7M/2B1YQsu6EPAk1V/tLkKiNwEadkAKNFUxZngGA==
```
### 3 拼接发送交易的数据
拼接 交易数据需要注意的是 msg、fee、memo 需要和签名的数据中的msgs 、fee、memo 保持一致
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
"fa9bUlNRA3qa9PEYR2py6CgpQbbqVsuKhJRowMdlf90byj7M/2B1YQsu6EPAk1V/tLkKiNwEadkAKNFUxZngGA==", //数据签名的base64格式
            "pub_key": {
                "type": "tendermint/PubKeySecp256k1",
                "value": "AjmQ01Z+IoHuKLdPaFzV6IJQB88ahW2qv2rEw2H4B5dq"  //bip32生成的地址的公钥
            }
        }],
        "memo": ""
    },
    "mode": "async"    发送交易的方式async 为异步，block 为同步
}
```
拼接好数据后，通过post的方式发送到/txs接口

关于常见错误的说明
```
{"codespace":"sdk","code":4,"message":"signature verification failed; verify correct account sequence and chain-id"
```
错位为签名验证失败
需要检查 
1 数据拼接的结构中字母的顺序是否为按照字母顺序顺序排列
2 公钥与地址是否匹配

## 五、查询交易是否成功
同步发送数据出块之后即可返回结果， 返回结果包含 error 属性或code 属性，均表示失败

异步发送数据，需要根据返回交易哈希，读取交易详情，分析交易详情判断交易是否成功

1 根据交易哈希获取交易详情
接口
http://URL/txs/{hash}

2 返回结果分析
返回结果包含 error 属性或code 属性，均表示失败

判断交易是否成功和解析错误信息代码举例
```
function assertOk (res) {
  console.log('assertOk')
  console.log(res)
  console.log('assertOk')
  if (Array.isArray(res)) {
    if (res.length === 0) throwErrorCode(errorList.Error_sending_transaction)

    res.forEach(assertOk)
  }

  if (res.error) {
    //需要检查  error 是不是josn
    /*
    {"error":"[{\"msg_index\":\"0\",\"success\":false,\"log\":\"{\\\"codespace\\\":\\\"dam\\\",\\\"code\\\":105,\\\"message\\\":\\\"lambda1md6hr4qtf62al2ls6ypp63kn0nxl35w6f7csde is not a miner\\\"}\"}]"}
    */
   if( res.error.indexOf("[{")==0 ){
    var msglist= JSON.parse(res.error)
    
     var log = msglist[0].log;
     
     var msg = JSON.parse(log)
     
     throw new Error(msg.message) 


   }
   
    throw new Error(res.error)
  }

  // Sometimes we get back failed transactions, which shows only by them having a `code` property
  if (res.code) {
    var message ;
    if(res.logs){
       message = res.logs.map((item) => {
        return item.log
      }).join(',')
      console.log(message)
    }else{

       var raw_log = JSON.parse(res.raw_log);
       message = raw_log.message;

    }
    
    
    throw new Error( JSON.stringify({code:res.code,message}) )
  }


  if (!res.txhash) {
    const message = res.message
    throw new Error(message)
  }

  return res
}
```

