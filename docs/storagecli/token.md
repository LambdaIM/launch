# storagecli token

## Description

Get token from storage provider

## Usage
```
storagecli token [command]
```

## Available Commands

| Name| Description                                                                   |
| --------------- | --------------------- 
| clear  |clear local tokens|
| list  |list local tokens|
| restore  |restore tokens from a secret|
| share  |create share tokens|
| sync  |Sync exist order's token|
| update  |Get operate token of order|


## Examples
```
./storagecli token  clear
clear tokens /root/.lambda_storagecli/localdb/meta

./storagecli token sync buy
Password to sign with 'buy':
sync orders begin, This may take some time...
http://182.91.242.11:13659/market/user/matchorders/lambda1sdxejrlwdjjuyjffcqxawh252kq28w8vgwlqgg
Order                                              Total                Used
A62C0765A24CB031686B06A6C1EB0F508E625F1E           15 GiB               7.8 GiB
sync orders finish

```
# list local tokens

## Usage
```
 storagecli token list tokens [flags]
```
## Flags

| Name, shorthand| Default   | Description | Required                                                                  |
| --------------- | ----   | -------- | --------------------- 
| --limit  | 100 | sorder limit to show |
| --order_id  | | specify a orderid to list tokens |
| --sync  |  |  sync [account] orders from chain |

## Examples

```
./storagecli token list teshare --order_id 2E5A78E1564E7D220C327B1EC4F7087AD7CF2708  
order : 2E5A78E1564E7D220C327B1EC4F7087AD7CF2708 ,has created 0 share token 	 type:  [share]
 |Permission |Expired                   |Bucket |Prefix
 |download   |2020-05-16T23:31:22+08:00 |test1  |go.sum_2225e463778249189a136c039479c728   |
 |download   |2020-05-17T00:08:21+08:00 |test1  |app.conf_1288cb3dec9346d6a6adb3ff0a73d16d | 
```
 
# restore tokens from a secret

## Usage
```
storagecli token restore ACCOUNT  [flags]
```
## Flags

| Name, shorthand| Default   | Description | Required                                                                  |
| --------------- | ----   | -------- | --------------------- 
| --secret  | secret | sync token from share secret |

## Examples
```
 LAMBDA_ORDER_ID=92F1918765F3654EE1E4F98BD64B96CB4DD4C0BC  ./storagecli token restore teshare --secret 8Le3ZHpTqX1NdNg6AKtCsm6YPHcxozRcr5Drybzofh3nUwR7kZiifdSRA4KAjn6bU3  
http://182.91.242.11:13659/market/user/matchorders/lambda1ejuhsxthm7kpjz63eczlg28prrfje9vd22ma3x
file download keys nums 1
```

# create share tokens

# Usage
```
storagecli token share ACCOUNT [remote path] [duration] --download  [flags]
```
## Flags

| Name, shorthand| Default   | Description | Required                                                                  |
| --------------- | ----   | -------- | --------------------- 
| --download  |  | add share token with download privilege |

## Examples
```
LAMBDA_ORDER_ID=5A8E65C1C04177234DC8E7B7DFBCE98CC31134AC  ./storagecli token share buy lamb://test/file50_e477d42cadc445049507f215142be187  1M2h3m4s  --download
Password to sign with 'buy':
create share token with these properties:
share duration: 722h3m4s
share path: lamb://test/file50_e477d42cadc445049507f215142be187
share type: [download]
please wait a few seconds
got share token secret:
2b7nqoMMBrKzEUrvz44yFWHUk3xRpBYtvy7seKpwjVdJz2iAnhBpJMiXghhkrXLqPD
```
