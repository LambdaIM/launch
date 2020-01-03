# The guide of Testnet 0.4.0 version for Miner 

Miner are associated with multiple storagenode 
The video guide of Testnet 0.4.0 version for Miner and Storagenode ：[https://pan.baidu.com/s/1j-defxC0y2gT_vKupwGcVA](https://pan.baidu.com/s/1j-defxC0y2gT_vKupwGcVA)



* [Miner Deployment：](#Miner-Deployment)
* [1. Download Package](#1Download-Package)
* [2. Miner Deployment](#2Miner-Deployment)
* [3. Add Account](#3Add-Account)
* [4. Create Miner](#4Create-Miner)
* [5. Register Storagenode](#5Register-Storagenode)
* [6. Configure-Storagenode](#6Configure-Storagenode)
* [7. Miner Create Sellorder](#7Miner-Create-Sellorder)
* [8. Create Buyorder](#8Create-Buyorder)
---
* [Mining and File Upload & View：](#Mining-and-File-Upload&View)
* [1. Mining Deployment](#1Mining-Deployment)
* [2. File Upload](#2File-Upload)
* [3. Miners Mining](#3Miners-Mining)
* [4. Mining reward ](#4Mining-Reward )
---
* [Withdraw order‘s reward ](#Withdraw-Order‘s-Reward )
* [Test Internet Connection](#Test-Internet-Connection)
* [1. Dht Connection Test](#1Dht-Connection-Test)
* [2. Miner Connection Test](#2Miner-Connection-Test)
* [3. Storagenode Connection Test](#3Storagenode-Connection-Test)
* [4. Validator Connection Test](#4Validator-Connection-Test)


# Architecture of Data Storage Business 
![avatar](arch_img/lamborage_arch.jpg)

# Miner-Deployment

## 1Download-Package

Download the installation package and extract the file  

```
mkdir -p ~/LambdaIM && cd ~/LambdaIM
```
Download the package 
```
wget https://github.com/LambdaIM/launch/releases/download/v0.1.2/lambda-storage-0.1.2-testnet.tar.gz
```
Extract the installation package 
```
tar zxvf lambda-storage-0.1.2-testnet.tar.gz
```
Enter the content after extracting
```
cd lambda-storage-0.1.2-testnet
```

## 2Miner-Deployment

```
./lambdacli config node tcp://47.93.196.236:26657

Select validator IP as below：
47.93.196.236
47.94.129.97
39.105.148.217

```

```
 ./lambdacli config chain-id lambda-chain-test4.2
```

```
./lambdacli config trust-node true
```
## 3Add-Account
Please replace [your-account-name]  with your custom account name. You need to set up your account and password without brackets. 
```
./lambdacli keys add [your-account-name]
```
Inserting the account which is created by wallet, or create account via wallet's mnemonic wording to opereate it. 
```
./lambdacli keys add [your-account-name] --recover
```
Enter the command and follow the instruction to enter your password and mnemonic wording 

## 4Create-Miner
Pledge on validator. Validator address can look up on the explorer here. http://testbrowser.lambda.im/#/ or you can discuss with validators. 
[your-account-name] is you account's name which you set up on step 3. 

### Create Miner
```
./lambdacli tx staking delegate lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl 20000000utbb \
--from [your-account-name] --broadcast-mode block -y
Select validator's address：
lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl
lambdavaloper1thj5fv8d0dsh3aealhpxm9mvgxjfh87suwuj2h
lambdavaloper1a83p8s9gs5hua09xn5ktmahepst3vzg9u2l20d
```

### Miner initiallization
[miner-name] is your account's name from step 3 creation, miner deployment can use the name of [miner-name] 
```
./lambdacli tx market create-miner --from [miner-name] --broadcast-mode block -y
```
### Start Miner-server
```
./lambdacli miner-server --from [miner-name] --query-interval 5 --laddr tcp://0.0.0.0:26670 --gas 500000 --daemonize --log.file [log_file_path]
```
And then enter miner's account and password to activate it. 

Attention: 

If you find your miners each block submit more than 5 mining proofs on explorer, you need pause miner-server process and increase the number of gas 
(Adjust the parameter of gas 500000 to 1000000) and restart: 
```
./lambdacli miner-server --from [miner-name] --query-interval 5 --laddr tcp://0.0.0.0:26670 --gas 1000000 --daemonize --log.file [log_file_path]
```

### View the miner service process 
```
./lambdacli miner-server --status
```
```
The return value as below which about the process is runing ：
2019/11/27 08:37:39 miner server is running as daemon, pid is 19678
```

### Stop Miner-server
```
./lambdacli miner-server --stop
```
```
The return value as below which is about stopping miner service successfully：
2019/11/27 08:38:51 miner server stoped
2019/11/27 08:38:51 miner server pid file /root/.lambdacli/daemon/miner_server.pid removed
```

## 5Register-Storagenode

Create and register Storagenode

machine-name：greater than 3 and less than characters,supports English capital letter and lowercase letter and numbers. Initial storagenode（`./storagenode init`）and then execute `./storagenode info` to look up dht-id and pub-key。

```
./storagenode init
```

```
./storagenode info
The result of execution：
storage name: machine1
  public key: 04e73c10925aafffdf524e8f39c745afa6b727fb0fa964552b70bef5aa473944b9d9a21d177bd02c7bfb7dccab7400edbd46da53d99690ab84100b4c21826d6c8e
      dht id: 3qs5EPz4EmnSHZD7rCJfg649bL6izHVundMi5HimWJWb
```

```
./lambdacli tx market create-machine --dht-id [dht-id] --name [machine-name] \
 --pub-key [pub-key] --from [miner-name] --broadcast-mode block -y
```


## 6Configure-Storagenode
[storagenode deployment activation reference](./Testnet0.4.0-Storagenode-configure-en.md)

## 7Miner-Create-Sellorder

The paid rate is 1 which define as ordinary sell order; the paid rate is greater and equal to 3 which is a high-quality sell order, and a high-quality sell order can specify the sell order price.  
Setting the specified storagenode‘s machine-name require to sell space size;  
The minimum of buying size(min-size)can not smaller than 1GB;  
The minimum of buying duration(min-buy-duration) can not smaller than 1 month;    
The maximum of buying duration(max-buy-duratiocan) not greater than 60 month.   
Reminder: Please palce a high-quality selling order with rate=3 on testnet, so that create the buying order can specify the selling order which martch with your own miner. 

### Create sell order

A storagenode only accept a selling order with available space.

```
./lambdacli tx market create-sellorder --price 5000000ulamb  \
--rate [rate] \
--size [size]GB \
--market-name LambdaMarket --machine-name [machine-name] \
--min-size [min-size]GB \
--min-buy-duration [min-buy-duration]month \
--max-buy-duration [max-buy-duration]month \
--from [miner-name] --broadcast-mode block -y
```
### Search sell order


```
Searching account's address：
./lambdacli keys show [miner-name] --address
According account address to look up miner's selling order：
./lambdacli query market miner-sellorders [address] [page] [limit] 

For example：
Searching account name as"miner2" address：./lambdacli keys show miner2 --address
The return value：lambda1k6rxrmly7hz0ewh7gth2dj48mv3xs9yz8ffauw

./lambdacli query market miner-sellorders lambda1k6rxrmly7hz0ewh7gth2dj48mv3xs9yz8ffauw 1 10
The return value：
SellOrder
  OrderId:            54F82FBD979BE150C8B3246D82DDF60F043129EE  //Sell order ID，cancel the selling order or create a high-quality buying order will use the ID
  Address:            lambdamineroper1k6rxrmly7hz0ewh7gth2dj48mv3xs9yznx96fn
  Price:              5000000
  Rate:               3.000000000000000000  //rate is greater or equal to 3，or the selling order is high-quality selling order
  Amount:
  SellSize:           400
  UnUseSize:          0
  Status:             1
  CreateTime:         2019-11-04 12:02:24.379880755 +0000 UTC
  CancelTimeDuration: 1h0m0s
  MarketAddress:      lambdamarketoper1thj5fv8d0dsh3aealhpxm9mvgxjfh87srk3887
  MachineName:        machine1
  MinBuySize:         1
  MinDuration:        720h0m0s
  MaxDuration:        43200h0m0s
```

### Cancel sell order

According to SellOrderID to cancel selling order 
```
./lambdacli tx market cancel-order [orderId] --from [miner-name] --broadcast-mode block -y
```


## 8Create-Buyorder
Miners can not buy own selling order, it can change to other accounts to place buying order. 

Create the high-quality buying order require specify the corresponding high-quality selling order SellOrderID.   
account-name is the current account's name;   
duration is the buying length of time;   
size is requiring buying space,can not less than minimum purchase space specified in the corresponding sell order

### Create the ordinary buying order 

```
 ./lambdacli tx market create-buyorder --from [account-name] \
 --duration [buy-duration]month --market-name LambdaMarket \
 --size [size]GB --broadcast-mode block -y
```

### Create the high-quality buying order 

```
./lambdacli tx market create-buyorder --sellorder-id [orderId] \
--from [your-account-name] --duration [buy-duration]month \
--market-name LambdaMarket --size [size]GB --broadcast-mode block -y
```
### Searching the match order 

```
Searching account address：
./lambdacli keys show [account-name] --address
According to the account address to look up the match order：
./lambdacli query market matchorders [address] [page] [limit]

For example：
./lambdacli keys show buyaccount --address
The return value：lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr
./lambdacli query market matchorders lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr 1 10
The return value：
MatchOrder
  OrderId:               05F09566BA4397BC9EB378EC202676D3FFCAF660   //Match order ID，uploading files will use the ID
  AskAddress:            lambdamineroper1k6rxrmly7hz0ewh7gth2dj48mv3xs9yznx96fn
  BuyAddress:            lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr
  SellOrderId:           58941CFFEEA859AED51172F0F9DF3E77293D2E12
  BuyOrderId:            F3B5BDE351253E1D47DA7CEB24C0E4BAB5BDA808
  Price:                 5000000
  Size:                  20
  CreateTime:            2019-11-01 13:20:58.296399278 +0000 UTC
  EndTime:               2019-12-01 13:20:58.296399278 +0000 UTC
  CancelTimeDuration:    1h0m0s
  WithDrawTime:          2019-11-01 13:20:58.296399278 +0000 UTC
  Status:                0
  MarketAddress:         lambdamarketoper1thj5fv8d0dsh3aealhpxm9mvgxjfh87srk3887
  MachineName:           machine1
  UserPay:               100000000ulamb
  MinerPay:              100000000ulamb
  PubKey:                PubKeyEd25519{5AD2B4ECA8C33922A8228A5217900E5725BF3013639118D1002B6A413971F9DC}
  PeerId:                bdd4da2a3021d30e8f215dba64716cec02cdb8a7
  DhtId:                 5i6fXKQJoktPVmt9PAfZ18RN7DG6tghQN7SK7A3Bq4Rc
```


# Mining-and-File-Upload&View

## 1Mining-Deployment

### Storagecli initialization 
```
./storagecli init
```
After storagecli Initialization and generate the default configuration file ~/.lamborage/config/user.toml，adjust  user.toml

```
[broker]
# dht_gateway_addr as validator dht service ip and port;
dht_gateway_addr = "39.105.148.217:13000"  ## dht address options:39.105.148.217:13000/47.94.129.97:13000/47.93.196.236:13000
# validator_addr as validator IP and port
validator_addr = "39.105.148.217:13659"   ## address options：39.105.148.217:13659/47.94.129.97:13659/47.93.196.236:13659
extra_key_file = " "

[gateway]
# local listen address
address = "0.0.0.0:9002"
# for login web UI
access_key = "accesskey"
secret_key = "secretkey"
```

### Synchronize MatchOrder Token

account-name is buying order's account name；
```
./storagecli token sync [account-name]
```


## 2File-Upload

Text/image/video/audio/executable files/compressed package files can be uploaded normally. 
The uploading the source file path will be the absolute path. 

- orderid is match order ID;
- account-name is buying order's account name；

- Use the following two parameters to  upload files as below: 
- - provider_storage_address is the configuration file ~/.lamborage/config/node.toml's gateway.address，the following example port 9000 is modified to the port as below
- - provider_node_address is the configuration file ~/.lamborage/config/node.toml'sserver.address，the follwoing example port 13000 is modified to the port


### Upload File

```
LAMBDA_ORDER_ID=[orderId] ./storagecli cp [account-name] [srcPath] lamb:// 

Match order ID is the storage validator on intranet: 
LAMBDA_ORDER_ID=[orderId] ./storagecli cp [account-name] [srcPath] lamb:// --provider_node_address [storagenode IP on intranet]:13000 --provider_storage_address [storagenode IP on intranet]:9000
```

Upload file error as：Error: Insufficient permissions to access this file xxx or please follow the execution：
1. Storage validator machine delete storagenode gateway's metadb: `rm -f ~/.lamborage/metadb`
2. Storage validator machine reactivate storagenode gateway service
3. Storagecli customer sever clear all history token: `./storagecli token clear`

### Look up Upload File List

```
LAMBDA_ORDER_ID=[orderId] ./storagecli ls [account-name] lamb:// 
```

## 3Miners-Mining

Each 1G file stored by miner will generate a corresponding statement. All statements are valid in 1 month. Each block generation cycle (about one block per 6 seconds) will initiate challenge from the consensus network. The miners challenge the statement successfully and submit a mining certificate. You will get the reward.


1. valid order and  valid storage file >= (1T)  miner with mining right;
2. Miner stored files are respectively 1/3/5G to generate corresponding 1/3/5 statement；
3. The more a miner statement, the greater the probability that the miner will be selected.


## 4Mining-Reward
Mining reward = increase  each block issuance  * （43% * 95% / the number of miners mining） +increase each block issuance  * （43% * 5% /the number of miners mining ）* proportion of the amount of miner's pledge on validator's pledge * 75%
```
For example, the additional issuance of a single block is 100LAMB. Only a node on the whole network pledges 666 TBB total. A total of 10 miners on the whole network pledge 1TBB and have 10 statements each.

The mining reward obtained by a single miner with a single block is 4.085 LAMB= 100LAMB * 43% * 95% / 10 + 100LAMB * 43% * 5% / 10 * 1/676 * 75%
```

# Withdraw-Order‘s-Reward
[withdraw selling order's reward by MatchOrderID](./docs/lambdacli/tx/market/withdraw-miner.md)  
[withdraw selling order's reward by StoragenodeName](./docs/lambdacli/tx/market/miner-withdraw-machine.md)

## Test-Internet-Connection

As activate dht、miner、storage node、validator upload files occur error, please activate debug for troubleshooting. 
### 1Dht-Connection-Test

```
./storagecli debug dht --address [dht.external_address]
```
### 2Miner-Connection-Test

```
./storagecli debug miner --address [miner server address]

```
### 3Storagenode-Connection-Test
Use “storagecli debug order” the order test uploading file, or gateway require to cease and add --debug parameter when activate with the latest installation package: 
`nohup ./storagenode gateway --debug >> sgateway.log 2>&1 &`

```
./storagecli debug order --provider_node_address [dht.external_address] --provider_storage_address [gateway.external_address]
```
### 4Validator-Connection-Test

```
./storagecli debug validator --address [validator address]
```
