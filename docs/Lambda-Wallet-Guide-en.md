# Lambda Wallet Wallet Instructions
Version 0.6.66

A wallet supports the creation and management of multiple accounts in Chinese and English.


Download ：[https://github.com/LambdaIM/launch/releases/tag/Wallet0.6.66](https://github.com/LambdaIM/launch/releases/tag/Wallet0.6.66)



![avatar](img/wallethome@2x.png)


* [Switch-Language](#Switch-Language)
* [Create-Account](#Create-Account)
* [Use-Mnemonic-Import-Account-Into-Lambda-Program](#Use-Mnemonic-Import-Account-Into-Lambda-Program)
* [Import-Account](#Import-Account)
* [Home-Page-Description](#Home-Page-Description)
* [Collect-test-token-of-test-network](#Collect-test-token-of-test-network)
* [Transfer](#Transfer)
* [Export-Account-Profile](#Export-Account-Profile)
* [Change-Validator-Node-IP](#Change-Validator-Node-IP)
* [Exchange-LAMB-For-TBB](#Exchange-LAMB-For-TBB)
* [View-Validator-Info-And-Pledges](#View-Validator-Info-And-Pledges)
* [View-Partner-Info-And-Pledges](#View-Partner-Info-And-Pledges)
* [Redelegate](#Redelegate)
* [Cancel-Pledge](#Cancel-Pledge)
* [Withdraw-Rewards](#Withdraw-Rewards)
* [Withdraw-Validator-Profit](#Withdraw-Validator-Profit)
* [Assets View&Trading](#Assets-View-And-Trading)
* [Proposal Deposit&Vote](#Proposal-Deposit-And-Vote)
* [Market and trading space](#Market-and-trading-space)
* [Open the lambdaS3 console](#Open-the-lambdaS3-console)
* [Switch between main network and test network](#Switch-between-main-network-and-test-network)
* [Mining sub account creation export import](#Mining-sub-account-creation-export-import)
* [Initialize miner](#Initialize-miner)
* [Mining Guide](#Mining-Guide)
* [Set gas price](#Set-gas-price)
* [Withdraw order Commission](#Withdraw_order_Commission)
* [Order renewal](#Order_renewal)
* [Market pledge](#Market_pledge)
* [Withdrawal of market pledge income](#Withdrawal_of_market_pledge_income)



 
## Switch-Language

![avatar](img/lang@2x.png)

## Create-Account
Click Create Wallet button to go to create wallet page.

Enter the wallet name, password, confirm the wallet password, and click the Create button to enter the mnemonic page.

![avatar](img/create@2x.png)

Please keep the mnemonic in order to restore the wallet later. It is best to record the mnemonic on the paper. The mnemonic can also be imported into the validator node program.

Click Next Step button to go to the next page. 

![avatar](img/word@2x.png)

On the page that confirms the mnemonic, click the word on the page in the order of the mnemonics just shown.

![avatar](img/select@2x.png)

After click the page shows as follows: 

![avatar](img/selectall@2x.png)

Click Export Keystore File to back up your wallet.

![avatar](img/file@2x.png)

Import the wallet again via lambda**********.keyinfo.

Create an account with your wallet completed here.


## Use-Mnemonic-Import-Account-Into-Lambda-Program

After creating the account, save the Mnemonic Words, use Mnemonic Words can import account into the lambda validator node.

Call the command line with lambdacli.

```bash
./lambdacli keys add [name] --recover
```

Enter the password twice according to the prompt.

```bash
Enter a passphrase to encrypt your key to disk:
Repeat the passphrase:
```
![avatar](img/zhujici.png)


If the address of the output account is consistent with the wallet, the import is successful.

**tips**
Please note the mnemonic words showed in picture is just an example. 





## Import-Account

Click import wallet in the home page to enter the page for import accounts.


![avatar](img/import1@2x.png)   

Click on Choose Wallet Files to select the backup file for your account.

The backup file is suffixed with keyinfo. For example, the configuration file created by the wallet is lambda.keyinfo.

Enter password when creating the wallet, then enter the name of the new wallet, and click import to import the wallet.

![avatar](img/import2@2x.png)   


According to the mnemonic word import account, fill in the mnemonic word and set the password.




## Home-Page-Description
Newly created account with a balance of 0 and no transaction history

![avatar](img/home2@2x.png)  

At the top is the navigation menu, click the Settings button to enter the settings page, click on the account address to copy it.

At the bottom is the information of the Validator node the wallet connected, including the public key address of the node, the height of the block, and the latest synchronized time of the block.

When account has a transaction record shows as follows

![avatar](img/home@2x.png)


## Collect-test-token-of-test-network

After logging into the wallet account, click the activity link on the home page
![avatar](img/WXceshicoinen.png)
Jump to 
[http://faucet.lambda.im/](http://faucet.lambda.im/)
![avatar](img/WXceshicoinget.png)
Enter the created lambda primary network address, for examplelambda163q4m634nq8les4nuvdvz49tk6aeh926t0**** 

Now it supports receiving LAMB and TBB of test network for storage mining test
Claim rules:
One IP can get 50000 LAMB and 5 TBB every day;
One lambda main network address, which can be picked up ten times and ten times respectively.




## Transfer
Click the Transfer button on the home page to open the Transfer dialog box and fill in the To address and amount.

![avatar](img/send@2x.png)

Click Next to preview the transaction information, you can modify the gas 
![avatar](img/send3@2x.png)
click OK. The dialog box for entering the wallet password is displayed, enter the wallet password.

![avatar](img/pasword@2x.png)

Click Submit, wait for 10s or so to complete the transfer, the transfer success is as follows

![avatar](img/ok@2x.png)

Click View Detail to view transfer details

![avatar](img/view@2x.png)


## Export-Account-Profile

Click Keystore File Backup on the settings page to view the account backup file.

![avatar](img/set@2x.png)


## Change-Validator-Node-IP
Click Switch Validator on the settings page to go to the page to view the Validator information.

![avatar](img/info@2x.png)

Change the Validator IP in the input box, click Submit, and the message is as follows:

![avatar](img/ok2@2x.png)


## Exchange-LAMB-For-TBB

TBB can be used for pledge

![avatar](img/duihuan1@2x.png)

![avatar](img/duihuan2@2x.png)


## View-Validator-Info-And-Pledges
![avatar](img/valist@2x.png)
First column is My Pledge List.
Second column is Validator List.

Click to Validator List

![avatar](img/valist2@2x.png)

Click to view the validator node details

![avatar](img/vainfo@2x.png)

Click on the pledge button to pledge

![avatar](img/zhiyainfo@2x.png)


## View-Partner-Info-And-Pledges
First column is My Pledge List.
Second column is Partner List.

![avatar](img/plist@2x.png)

Click the Partner List to view all the partner information.

![avatar](img/plist2@2x.png)

Click to view partner details

![avatar](img/pinfo@2x.png)

Click on the pledge button to pledge

![avatar](img/zhiya2@2x.png)

## Redelegate
Click on the Redelegate button on the details page of the node
![avatar](img/WXrv1@2x.png)
Click to open the Redelegate window

Fill in the number of TBB  that need to be re-pledged and select a new node.

(If we want to redelegate all tbbs, we may fail. It is suggested that the total amount of pledge - 0.1 TBB is easier to be redelegated successfully.)


![avatar](img/WXr2@2x.png)

## Cancel-Pledge
Click the Cancel pledge button on the node's details page.
![avatar](img/cancel1@2x.png)
Click to open the cancel pledge window
![avatar](img/cancel2@2x.png)
Fill in the number of tbbs that need to be cancel.

(If you want to cancel all tbb, it may fail, it is recommended that the total amount of pledge -0.1 tbb to cancel pledge is easier to succeed)


## Withdraw-Rewards

![avatar](img/wi@2x.png)
![avatar](img/wi1@2x.png)

## Withdraw-Validator-Profit
On the home page, click on the Withdraw Validator Profit in the Withdraw Rewards menu.

![avatar](img/wv1@2x.png)

You can open a window to withdraw the benefits of the node.

![avatar](img/wv2@2x.png)

## Assets-View-And-Trading

Click on the asset label on the front page of your wallet to see all assets in your current account.
![avatar](img/asset1@2x.png)
Click on the trade button to open the window for trading assets.
![avatar](img/asset2@2x.png)

## Proposal-Deposit-And-Vote
Click on the proposal in the navigation menu at the top to enter the proposal list page.
![avatar](img/t1@2x.png)
Click on the text description section of the proposal to enter the proposal details page.
![avatar](img/t2@2x.png)

When the status of the proposal is DepositPeriod, the proposal can be deposited with lambs.
Click the deposit button to open the deposit dialog box
![avatar](img/t3@2x.png)
When the deposit meets the requirement, the proposal will enter the VotingPeriod and click the voting button to open the voting dialog box.

![avatar](img/t4@2x.png)
Voting may choose to Yes, No, No with Veto or Abstain.  
If the first vote is incorrect, it doesn't matter that the second vote will cover the result of the first.  
The weight of voting is equal to the amount of pledge, which is valid in both node pledge and partner pledge.  
If there is no pledge, the voting is invalid.  
## Market-and-trading-space


Click the market link in the navigation bar to enter the market page.


#### My order list The order list contains buy and sell orders

![avatar](img/WXmk1@2x.png)

Purchase space

There are two ways to buy space. One is to automatically match the purchase, and the other is to choose a miner to buy the premium.

The automatic match purchase is for a sell order with an odds price of 5 lamb.

The selected high-quality sell order is a sell order with an odds of more than 3 and a unit price greater than 5lamb.

![avatar](img/WXmk2@2x.png)

Automatically match the purchase space only needs to fill in the size and duration of the space, such as buying 2gb 3 months space

![avatar](img/WXmk7@2x.png)

To buy a miner's premium purchase order, you need to select a miner to check whether the minimum purchase space, the shortest time, and the longest time of the order meet your needs. If you meet the requirements, you can purchase it by filling in the space and duration.

![avatar](img/WXmk15@2x.png)


#### Space for sale
The account is a miner's account and a list of sell orders for this account in the market will be listed here.
 
![avatar](img/WXmk3@2x.png)
After creating a Storage node in the mining program, you can place a sell order for the Storage node in your wallet.

For example, the command to create a Storage node


./lambdacli tx market create-machine  \

--dht-id HL4oGXqDQDMHyKpRWwxF9UmcnVvhxueDnghWu7zuMKMH \
  
--name machine1  \

--peer-id 3830e6d38b9e03ae6653 \ 
 
--pub-key 1624de64201c233b87da4a2d27210ecb923e45ad0b8343352b0ab22ee9d5abbe9bdededd9b \

--from test1 \
 
--broadcast-mode block -y

In the pop-up dialog box, select the Storage node and fill in the size of the space to be sold. （Only one sales order can be attached to a storage node. It is recommended to sell all the space at one time）.

Odds, unit price There are also restrictions on the user's purchase conditions, the minimum purchase space, the shortest time, the longest time

About odds
Odds = 1 can not specify the price, can only be 5LAMB/G/month

Odds >=3 requires a specified price, price >=5LAMB/G/month

Odds = 1 for regular sell orders, odds >= 3 for premium sell orders

Only high-quality sell orders will appear in the market list for users to choose, ordinary buy orders can only be automatically matched


![avatar](img/WXmk8@2x.png)




Click on the order list page to view the details page of the order.
 
  Selling order details page
 
![avatar](img/WXmk4@2x.png)

## Open-the-lambdaS3-console



After purchasing the order, you can use the lambdaS3 console to upload and download files and use the storage space.

![avatar](img/WXmk12@2x.png)
If you need to use the space of this order, you can upload files to space and delete files in the lambda storage.

Click to open the console button, pop-up window authorization dialog, you can complete the authorization of this order

![avatar](img/WXmk14@2x.png)

On the login page, enter:

Lambda Storage Console login information prompted in wallet: access-key: lambda, secret-key: 12345678
Complete login

![avatar](img/WXs32@2x.png)

You can upload the file, and drag the file to the file list area to upload the file.

![avatar](img/WXs31@2x.png)

## Switch-between-main-network-and-test-network

After logging in the wallet, click the network type on the left side of the footer to enter the node selection page

![avatar](img/enSwitchnetwork.png)

Click the default main network IP and then click submit to switch to the main network.

Click the default test network IP and then click submit to switch to the test network

## Mining-sub-account-creation-export-import

On the homepage of wallet, click mining, wizard and next until you see the module of creating sub account

![avatar](img/ensonaccount.png)

You can see the create miner sub account and import button

### Create sub account
Click the create sub account button to open the create sub account pop-up window

![avatar](img/encreatsubaccount.png)

To create a miner's sub account, you need to input the mnemonic words and password of the current wallet, and input the notes for easy memory

You can also import the sub account exported by wallet or blockchain program

### Import sub account
If you have a sub account JSON file, you can import the sub account through the wallet. If you have done the above operation, you can skip this step.

Click the import button to open the import sub account pop-up window

![avatar](img/enimportsubaccount.png)

To import a sub account, you need to select the JSON file of the sub account and the password of the current wallet

### Export sub account
If you need to use the mining sub account in the miner management program or blockchain program, you can export the sub account

![avatar](img/enexportsubaccount.png)

To export a sub account, you need to enter the password of the current Wallet

For example, select the sub account of wallet export in the miner management program
![avatar](img/sonaccountd5.png)

## Initialize-miner

Click the mining guide in the navigation menu, and click next on the mining guide page until you see the initialization miner module
Click the miner initialization button to open the create miner pop-up window
![avatar](img/enminersetup.png)

To create a miner, you need to select the sub account in the wallet and deploy the dhtid of the miner server
A dhtid of miner service can be obtained in miner management program
for example

![avatar](img/marketd3.png)

## Choose-to-use-wallet-identity-role

The first time you install and use the wallet, it will pop up automatically. Then you need to switch the identity. Click the Edit button of the role on the setting page to open the pop-up window
![avatar](img/enrole.png)

Select different roles and use slightly different functions
#### Wallet user
View assets, transfer, pledge mining, proposal voting, withdraw pledge reward

#### Space users
View assets, transfer, pledge mining, proposal voting, purchase space, use lambdas3, withdraw pledge reward

#### Miner
View assets, transfer, pledge mining, proposal voting, market trading space, mining guide, withdraw pledge reward, withdraw deposit mining reward

#### Verification node
View assets, transfer, pledge mining, proposal voting, withdraw pledge reward, extract node income


## Mining-Guide
Select miner role to use wallet, and you can see the menu of mining guide in the navigation menu

![avatar](img/enMiningGuide.png)
The mining guide shows the steps of mining,

In addition, the functions of the wallet and the instructions of the miner's management program are sorted out

The functions of wallet included in mining guide include

1 mining by pledge

2 create miner sub account

3 initialize miner

4 space for sale


## Set-gas-price

Click Edit gas price on the setting page and open the pop-up window to set gas price
![avatar](img/engaseprise.png)


## Withdraw_order_Commission

Click transaction on the homepage of wallet, click to withdraw order Commission
![avatar](img/txen.png)

Open the pop-up window to extract order revenue
![avatar](img/Orderrevenueen.png)
Withdrawal order revenue is the revenue in batch withdrawal order
Revenue from 100 orders per withdrawal
If there are many orders, you can try paging areas, such as extracting the first page, extracting the second page,
The extraction rules are as follows
Every 100 orders are 1 page, with a large number of orders. The page number can be filled in as 1, 2, 3, 4, 5, 6, etc
Only 100 orders can be withdrawn at a time
Extraction operation time limit 1 hour
The revenue in the order is calculated once every 24 hours. If the withdrawal is initiated within 24 hours, the amount withdrawn is 0

## Order_renewal

The usage time of the order needs to be increased, which can be realized by order renewal. On the order details page, click the order demand button to open the dialog box
![avatar](img/Ordertimeen.png)
The renewal price is the same as the purchase space,
Order cannot be renewed after expiration


## Market_pledge
Click the market pledge button on the home page to open the market pledge description page

![avatar](img/mp1.png)

Only the market created by users can be pledged. 

The default lambdamarket cannot be pledged

Minimum amount of market pledge 1000 lamb

Allow to pledge in multiple markets
Users can participate in the operation of the market created by users through pledge.

Market revenue is composed of Commission for registration, commission for completion and Commission for renewal.

Each income in the market will be distributed according to the market pledge proportion.

Income distribution rules:

Market creator receives 10% of market revenue

The market pledgor allocates the remaining 90% according to the pledge proportion (the market creator is also in the distribution set)

Click the market pledge button to open the market pledge dialog box to pledge

![avatar](img/mp2.png)

## Withdrawal_of_market_pledge_income

![avatar](img/mp3.png)

Click extract market revenue in the drop-down list of home 

transaction to open the dialog box for extracting market revenue

Select the pledge market, and then click next to extract the market pledge income

![avatar](img/mp4.png)









































