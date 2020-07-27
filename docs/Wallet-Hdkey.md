# 钱包账户信息、签名、配置文件说明
## 1 地址、助记词、加密算法相关
      生成助记词 使用 bip39   钱包和区块链使用长度为256 的24个单词

      生成hd钱包 使用bip32  derivePath 为  '44\'/364\'/0\'/0/0'

      钱包生成的地址和链生成的地址保持一致 需要使用相同的 derivePath

例如

js 例子

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
  根据公钥生成地址
 

   生成地址对生成的公钥 进行sha256 加密后，在用Ripemd160 处理， 在用bech32 添加 lambda 对应的前缀

例如  lambda 地址前缀 为lambda：`lambda1z4hs23xwjuudm44nhgcde0zxf5y63su8deuqs3`

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
 lambda  其他角色  前缀  

Bech32PrefixAccAddr = lambda                //lambda 地址前缀

Bech32PrefixAccPub = lambdapub              //lambda 公钥前缀 

Bech32PrefixValAddr = lambdavaloper         //lambda 操作地址前缀 

Bech32PrefixValPub = lambdavaloperpub   

Bech32PrefixConsAddr = lambdavalcons

Bech32PrefixConsPub = lambdavalconspub

Bech32PrefixMinerAddr = lambdamineroper      //lambda 矿工操作地址前缀

Bech32PrefixMinerPub = lambdamineroperpub

Bech32PrefixMarketAddr = lambdamarketoper

Bech32PrefixMarketPub = lambdamarketoperpub

## 2 数据签名相关
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
## 3创建矿工子账户
挖矿需要先创建矿工子账户，用于挖矿相关的业务处理，子账户的功能主要用于打包pdp相关

提交挖矿证明，是高频交易，以免干扰到用户对于账号的正常交易操作

创建矿工子账户和创建账户的助记词一致，

主账户的     derivePath 为  '44\'/364\'/0\'/0/0'

矿工子账户 derivePath 为  '44\'/364\'/0\'/0/1'  

## 4钱包配置文件加密解密说明
以js为例子

### 加密的过程
```
const crypto = require('crypto');
const bcrypt = require('****/bcryptjs');
 //修改过的bcrypt，需要能够支持传入随机数
const saltRounds = 12;
exports.ExportprivateKey = function encodePrivateKey(privatekey, password) {
	  var usersalt = crypto.randomBytes(16);
       //生成随机数
	

	  var salt = bcrypt.genSaltSync(saltRounds, '', usersalt);
        //用bcrypt根据随机数生成随机盐
	

	  var hash = bcrypt.hashSync(password, salt);
        //用bcrypt根据根据密码和随机盐生成哈希
        
	  const hashs = crypto.createHash('sha256');
	  hashs.update(Buffer.from(hash));
	  const userkey = hashs.digest('hex');
       // 使用sha256 对哈希进行处理生成key
	
      //
	  格式转换的方法，私钥对应praviteFB， key 对应userkeyFB
       //调用加密方法进行加密
	  var cryptoResult = encryptSymmetric(praviteFB, '', userkeyFB);
       /*
       encryptSymmetric 是tendermint 中的一个加密用的方法，
    https://github.com/tendermint/tendermint/blob/3e1516b62427aba1199766fc98943dffe81d7f4b/crypto/xsalsa20symmetric/symmetric.go
       */
	  var Key = toBuffer(cryptoResult);
	  return {
	    salt: usersalt,
	    privateKey: Key
	  };
	};
```
### 解密的过程
```
const saltRounds = 12;
exports.importPrivateKey = function decodePrivateKey(privatekey, usersalt, password) {
	  var salt = bcrypt.genSaltSync(saltRounds, '', usersalt);
       // bcrypt 根据随机数生成随机盐
	  var hash = bcrypt.hashSync(password, salt);
	   // bcrypt 根据密码和随机盐生成哈希

	  const hashs = crypto.createHash('sha256');
	  hashs.update(Buffer.from(hash));
	  const userkey = hashs.digest('hex');
       //使用sha256 对哈希值进行处理生成key
	
      /**
      js格式转换
      privatekeyFB 对应私钥privatekey
      userkeyFB   对应 key userkey
      **/
	

	  var seed = decryptSymmetric(privatekeyFB, '', userkeyFB);
      /**
      decryptSymmetric  是tendermint 中的一个解密用的方法，
    https://github.com/tendermint/tendermint/blob/3e1516b62427aba1199766fc98943dffe81d7f4b/crypto/xsalsa20symmetric/symmetric
      **/ 
	  if (seed == null || seed.length == 0) {
	    throw new Error('Password error');
	  }
	  var privateKey = toBuffer(seed).slice(5);
	  return privateKey;
	};
```
### 配置文件的解释与说明
```
{
	"salt": "bXJ0fCwdyta3LYtShoBrSA==",
	"privateKey": "Tghm8vmEY+XtA0IrwGhsm1RM2+WZG+6MvnK34cCM+unP6wC11Uy00Z5q3NiozF91DoIDFgBIEVD0XqSKv+2xjAKDU9WAhS8r1tpKs2A=",
	"name": "钱包的名称",
	"address": "lambda17ydyaapgwfp0ekgxmr74szjakn58h79rdyf7a3",
	"publicKey": "lambdapub1addwnpepqvyxh8rxtjymsqty8wkct8hjgf87ueqdrvgpr758x2p32jypzqmcxx269sx"
}
```
配置文件中的publicKey是带有lambdapub前缀的处理过程如下
```
const bech32 = require('bech32');
var Amino = require('****/amino.js');
const PREFIX = 'lambdapub';
Amino.RegisterConcrete(null, 'tendermint/PubKeySecp256k1');

function getAddress(publicKey) {
	  var PubKeyAmino = Amino.MarshalBinary('tendermint/PubKeySecp256k1', publicKey);
//通过Amino 库处理公钥 
//https://github.com/tendermint/go-amino
	

	  const words = bech32.toWords(PubKeyAmino);
        
	
       //通过bech32 添加前缀
	  return bech32.encode(PREFIX, words);
	}
```
从配置文件中带有前缀的公钥解出公钥过程如下
```
function getBytes(publicKeybech32) {
	  const decoded = bech32.decode(publicKeybech32);
	
	  var publicKeyAmino = Buffer.from(bech32.fromWords(decoded.words));
	  var publicKey = Amino.unMarshalBinary('tendermint/PubKeySecp256k1', publicKeyAmino);
	  return publicKey;

	}
```

## 4转账交易举例
 
 [查看更多交易说明](Wallet-API.md) 

 发送交易分为三个部分

### 第一部分拼接交易的数据结构
不同的交易类型，masgs 的结构会有差别
```
{
    "account_number": "1",  //通过用户信息获取
    "chain_id": "lambda-chain-test2.5", //链的版本号 通过最新的区块信息获取 
    "fee": {//手续费
        "amount": [{
            "amount": "101745",
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
每次发起交易前，均要通过账户信息接口获取最新的sequence

chain_id 可以通过 节点信息接口 /node_info 获取

### 2对拼接好的数据进行签名
例如 对上面字符串签名的结果为的base64
```
fa9bUlNRA3qa9PEYR2py6CgpQbbqVsuKhJRowMdlf90byj7M/2B1YQsu6EPAk1V/tLkKiNwEadkAKNFUxZngGA==
```
### 3 拼接发送交易的数据
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
## 5 灵活的预估交易需要gas
[更多交易说明见](Wallet-API.md) 

以转账交易为例

接口
```
/bank/accounts/${senderAddress}/transfers
类型 post
发送数据类型 json
```
post 数据的格式
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
