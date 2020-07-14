# lambdacli query market sellorders

## Description

Query market sell orders 

## Usage
```
 lambdacli query market sellorders [marketName] [orderType] [statusType] [page] [limit] [flags]
```

Print help messages:
```
lambdacli query market sellorders -h
```

## arguments

| Name               | type   | Required |  Description                                                         |
| ------------------ | -----  | -------- |  ------------------------------------------------------------------- |
| [marketName]       | string | true     |  Specify a market name in block chain, example: lambdamarket | 
| [orderType]        | string | true     |  Can use  `premium` or `normal` or `all`  |
| [statusType]       | string | true     |  Can use  `active` or `unActive` or `whole`|


## Unique Flags

| Name, shorthand    | type   | Required | Default  | Description                                                         |
| ------------------ | -----  | -------- | -------- | ------------------------------------------------------------------- |
| --node-status      |        | true     | ""       | query with miner node status | 

## Examples

Query markets sell order by orderType 
```
lambdacli query market sellorders LambdaMarket premium whole 1 100 --node-status
```

### Description

|  Field    | Description  |
| --------- | ------------ | 
|  NODE     | show node status with Online or Offline   |  
|  ID       | sell order id       | 
|  MIN_BS   | Minimum purchase space       | 
|  MIN_BT   | Minimum purchase time       | 
|  MAX_BT   | Maximum purchase time       |
|  ADDR     | Miner Address       |  

result:
```
NODE     ID                                         PRICE    RATE     TOTAL    AVAIABLE STATUS   CREATE_TIME          MIN_BS   MIN_BT   MAX_BT   ADDR
Offline  044F8AD3D77887261FCE2941C2F82A2BCC17DEAD   5LAMB    1.00     200      200      0        2020-03-18,02:11:16  10       30DAYS   600DAYS  lambdamineroper1h29mncmlezu2jsrsyvsg7vmd9zq8nt7505vwun

```
