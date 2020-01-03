# The guide of Testnet 0.4.0 version for Miner 

Miner are associated with multiple storagenode 
The video guide of Testnet 0.4.0 version for Miner and Storagenode ：[https://pan.baidu.com/s/1j-defxC0y2gT_vKupwGcVA](https://pan.baidu.com/s/1j-defxC0y2gT_vKupwGcVA)


* [Clear History Data](#Clear-History-Data)
* [Miner Deployment：](#Miner-Deployment)
* [1. Download Package](#1Download-Package)
* [2. Lambdacli Deployment](#2Lambdacli-Deployment)
* [3. Add Account](#3Add-Account)
* [4. Create Miner](#4Create-Miner)
* [5. Register Storagenode](#5Register-Storagenode)
* [6. Configure Storagenode](#6Configure-Storagenode)
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

# Clear-History-Data
Clear storagecli and storagenode data
```
rm -rf ~/.lamborage
```
**Tips**
If `~/.lamborage/config/node.toml` data_dir and mining_dir value is not default, clear data in the setting directory

# Miner-Deployment

## 1Download-Package

Download the installation package and extract the file  

```
mkdir -p ~/LambdaIM && cd ~/LambdaIM
```
Download the package 
```
wget https://github.com/LambdaIM/launch/releases/download/Storage0.2.1/lambda-storage-0.2.1-testnet.tar.gz
```
Extract the installation package 
```
tar zxvf lambda-storage-0.2.1-testnet.tar.gz
```
Enter the content after extracting
```
cd lambda-storage-0.2.1-testnet
```

## 2Lambdacli-Deployment

```
./lambdacli config node tcp://47.93.196.236:26657

Select validator IP as below：
47.93.196.236
47.94.129.97
39.105.148.217
182.92.66.63
```

```
 ./lambdacli config chain-id lambda-chain-test4.3
```

```
./lambdacli config trust-node true
```
## 3Add-Account
Please replace [your-account-name]  with your custom account name. You need to set up your account and password without brackets. 

Miner sub account is used to submit PDP Statement and PDP Proof. Every transaction need gas fees, the balance of the sub account must greater than 1000TBB.

**Tips**
You can also use Lambda Wallet to add miner account, import or export miner sub account, transfer, delegate.

### Add Miner Account and Miner Sub Account
```
./lambdacli keys add [your-account-name] --generate-miner 
```
Inserting the account which is created by wallet, or create account via wallet's mnemonic wording to opereate it. 
```
./lambdacli keys add [your-account-name] --recover --generate-miner 
```
Enter the command and follow the instruction to enter your password and mnemonic wording 

### Just Create Miner Sub Account when Miner has exists
```
./lambdacli keys create-miner [your-account-name] 
```
Enter the command and follow the instruction to enter your mnemonic wording


## 4Create-Miner
Pledge on validator. Validator address can look up on the explorer here. http://testbrowser.lambda.im/#/ or you can discuss with validators. 
[your-account-name] is you account's name which you set up on step 3. 

### Delegate to Validator
```
./lambdacli tx staking delegate lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl 20000000utbb \
--from [your-account-name] --broadcast-mode block -y
Select validator's address：
lambdavaloper1prrcl9674j4aqrgrzmys5e28lkcxmntxuvjpcl
lambdavaloper1thj5fv8d0dsh3aealhpxm9mvgxjfh87suwuj2h
lambdavaloper1a83p8s9gs5hua09xn5ktmahepst3vzg9u2l20d
lambdavaloper1r340rrv9fs95gqy5087e2mtz82vvwrglt6amx3
```

### Miner initiallization
```
./minernode init
```
After initializing "minernode", a default configuration file `~/.lambda_miner/config/config.toml` is generated, and then modified: config.toml

```
# Binding Addresses required for service startup
# For example when intranet IP is 192.168.10.10，public IP 200.200.200.100 
[server]
# Intranet network address, which can be mapped to "kad.external_address" port, please choose the port by yourself
address = "192.168.10.10:13000"
# Intranet network address, provided for StorageNode
private_address = "192.168.10.10:13001"
debug_log_traffic = "false"

[kad]
# DHT seed node address provided by lambda, multiple addresses can be configured
# Optional DHT address：39.105.148.217:13000/47.94.129.97:13000/47.93.196.236:13000/182.92.66.63:13000
bootstrap_addr = ["47.94.129.97:13000"]
# time you would wait to connect dht seed node
bootstrap_backoff_max = "30s"
bootstrap_backoff_base = "1s"
db_path = "/root/.lambda_miner/kademlia"
# this should listen at Public IP
## Public network address
external_address = "200.200.200.100:13000"
alpha = 3

[kad.routing_table_config]
bucket_size = 20
replacement_cache_size = 5

[api_key]
#root access key，can not be null
root_secret_seed = "yah"

[log]
level = "info"
output_file = "stdout"

[db]
# db config
lru_cache = "131072"
keep_log_file_num = "100"
write_buffer_size = "134217728"
recycle_log_file_num = "0"
target_file_size_base = "268435456"
max_write_buffer_number = "4"
max_bytes_for_level_base = "4294967296"
level_0_stop_writes_trigger = "24"
target_file_size_multiplier = "1"
max_background_compactions = "2"
max_bytes_for_level_multiplier = "2"
level_0_slowdown_writes_trigger = "17"
level_0_file_num_compaction_trigger = "8"
level_compaction_dynamic_level_bytes = "0"
compaction_algorithm = "0"
rate_bytes_per_sec = "10240"
data_backup_path = ""
data_backup_interval = "300000000000"
```

### Get Miner Sub Account Address
Rename [your-account-name]_miner_key.json to `default_miner_key.json` and move it to directory `~/.lambda_miner/config/`:
```
mv [your-account-name]_miner_key.json ~/.lambda_miner/config/default_miner_key.json
```

Query miner sub account address:
```
./minernode show-address 
Return value：
Master Address: lambda1fzeqzcemyye2qx2338clwss7nx3ukr7rx88snz //矿工账户地址
Miner Address: lambda1wgdcvew36nqwm2d5gj6yxraayjvnhfpf5rrfww  //矿工子账户地址
```

### Transfer LAMB to Sub Account
[miningAddr] is miner sub account address.
```
./lambdacli tx send [miningAddr] 1000000000ulamb --from [your-account-name] --broadcast-mode block -y
```

### Create Miner
[miner-name] is your miner's name。  
[miningAddr] is miner sub account address.
[dht-id] get with command `./minernode info`
```
./minernode info
Return Value：
                dht id: CdZsGtfsXVjMgt51EnaGAqr78YmgFxYsCAn4ubR1Dpgo //dht-id will be used when create-miner
        server.address: 0.0.0.0:14000
  kad.external_address: 182.92.242.59:14000
    kad.bootstrap_addr: [182.92.242.59:13000]
server.private_address: 127.0.0.1:14001

Create Miner：
./lambdacli tx market create-miner --dht-id [dht-id] --mining-address [miningAddr] --from [miner-name] --broadcast-mode block -y
```
### Start Miner
[log_file_path] is full path of miner log
```
./minernode run --query-interval 5 --daemonize --log.file [log_file_path]

If [your-account-name]_miner_key.json not moved to ~/.lambda_miner/config/default_miner_key.json，then add param --key-file to start：
./minernode run --query-interval 5 --daemonize --log.file [log_file_path] --key-file [filepath/your-account-name]_miner_key.json

```

### View the miner service process 
```
./minernode run --status
```
```
The return value as below which about the process is runing ：
minernode.pid is running, pid is 19276
```

### Stop Miner
```
./minernode run --stop
```
```
The return value as below which is about stopping miner service successfully：
stop daemon process from minernode.pid:19276 successfully
```

## 5Register-Storagenode

Create and register Storagenode

Initial storagenode:

```
./storagenode init
```

## 6Configure-Storagenode
[storagenode deployment activation reference](./Testnet0.4.3-Storagenode-configure-en.md)

## 7Miner-Create-Sellorder

When add param --normal, the paid rate is 0.5 which define as ordinary sell order, the price can only be 5000000ulamb;   
if not added, the paid rate is 1 which is a high-quality sell order, and a high-quality sell order can specify the sell order price equal or greater than 5000000ulamb.  
Setting the specified  sell space size;  
The minimum of buying size(min-size)can not smaller than 1GB;  
The minimum of buying duration(min-buy-duration) can not smaller than 1 month;    
The maximum of buying duration(max-buy-duratiocan) not greater than 60 month.   
Reminder: Please palce a high-quality selling order with rate=1(not add --normal param) on testnet, so that create the buying order can specify the selling order which martch with your own miner. 

### Create sell order

A storagenode only accept a selling order with available space.

```
./lambdacli tx market create-sellorder --price 5000000ulamb  \
--normal \
--size [size]GB \
--market-name LambdaMarket \
--min-size [min-size]GB \
--min-buy-duration [min-buy-duration]month \
--max-buy-duration [max-buy-duration]month \
--from [miner-name] --broadcast-mode block -y
```

### Create high-quality sell order

A storagenode only accept a selling order with available space.

```
./lambdacli tx market create-sellorder --price 5000000ulamb  \
--size [size]GB \
--market-name LambdaMarket \
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
  Rate:               1.000000000000000000  //rate is greater or equal to 1，or the selling order is high-quality selling order
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
After storagecli Initialization and generate the default configuration file `~/.lambda_storagecli/config/user.toml`，adjust  user.toml

```
[broker]
# dht_gateway_addr as validator dht service ip and port;
dht_gateway_addr = "39.105.148.217:13000"  ## dht address options:39.105.148.217:13000/47.94.129.97:13000/47.93.196.236:13000
# validator_addr as validator IP and port
validator_addr = "39.105.148.217:13659"   ## address options：39.105.148.217:13659/47.94.129.97:13659/47.93.196.236:13659

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
- bucket-name  greater than 3 and less than characters, you can create multiple bucket below one match order 


### Upload File

```
Create Bucket:
LAMBDA_ORDER_ID=[orderId] ./storagecli mb [account-name] lamb://[bucket-name]/

Upload File:
LAMBDA_ORDER_ID=[orderId] ./storagecli cp [account-name] [srcPath] lamb://[bucket-name]/ 

```

Upload file error as：Error: Insufficient permissions to access this file xxx or please follow the execution：
1. Storage validator machine delete storagenode gateway's metadb: `rm -f ~/.lamborage/metadb`
2. Storage validator machine reactivate storagenode gateway service
3. Storagecli customer sever clear all history token: `./storagecli token clear`

### Look up Upload File List

```
LAMBDA_ORDER_ID=[orderId] ./storagecli ls lamb://[bucket-name]/ 
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
[withdraw multiple selling order's reward](./docs/lambdacli/tx/market/miner-withdraw-count.md)


