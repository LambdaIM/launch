# lambdacli tx dam user buy

## Introduction

Create an buy order from digital asset market

## Usage

```
lambdacli tx dam user buy [flags]
```

Print help messages:
```
lambdacli tx dam user buy --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |
| --ask-address | string | true     | ""       |  The address of order's seller(means pledge record here) |
| --duration | string | true     | ""       |  The duration of the match order you could use |
| --size | string | true     | ""       |  The size of order you want to buy |
| --asset | string | true     | ""       |  The asset related to the digital asset market |

## Examples

```
lambdacli tx dam user buy --duration 1month --size 100GB --ask-address lambdamineroper10gat77jd5ucz7gw0m3xac8jfj5l83r6c0mswdj --asset uabc --from master
```

Output:

```
Response:
  Height: 19
  TxHash: 4A3BD5B15D6D56A85A5B9B42F8B50E102DAF60913A2EA8A1902F3D9AD917B2B0
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 41628
  Tags:
    - action = damCreateBuyOrder
    - address = lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
    - miner = lambdamineroper10gat77jd5ucz7gw0m3xac8jfj5l83r6c0mswdj
    - asset = uabc
	- cost = 10000000
    - matchOrderID = 65F21496016CDF70F165E32FB9FC43B5B19B87CA
```

# lambdacli tx dam user renew

## Introduction

Renew a match order by order ID

## Usage

```
lambdacli tx dam user renew [orderID] [duration] [flags]
```

- `orderID`: order ID of the match order
- `duration`: period to extend the match order

Print help messages:
```
lambdacli tx dam user renew --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx dam user renew 65F21496016CDF70F165E32FB9FC43B5B19B87CA 1month --from master
```

Output:

```
Response:
  Height: 5494
  TxHash: BEE63DE7E763BD40ED7FFF48B5C95A8CFCD1A082244BE9BC1D51F966F24178FE
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 41144
  Tags:
    - action = damOrderRenewal
    - address = lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
	- cost = 10000000
```

# lambdacli tx dam user transfer

## Introduction

Transfer ownership of file from order buyer to receiver

## Usage

```
lambdacli tx dam user transfer [orderID] [file] [flags]
```

- `orderID`: order id of the match order
- `file`: file path to transfer

Print help messages:
```
lambdacli tx dam user transfer --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx dam user transfer 65F21496016CDF70F165E32FB9FC43B5B19B87CA bucketName/fileName4 --receiver lambda1d93vleu5x42u5jv25amqg4e73hsnmhxhp3wznd --from master
```

Output:

```
Response:
  Height: 218
  TxHash: D9D9EE2871D9073371A796DC87F47699474AE5D48684D1D4459AF5DB5364978B
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 19079
  Tags:
    - action = transferOwnership
    - sender = lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
    - receiver = lambda1d93vleu5x42u5jv25amqg4e73hsnmhxhp3wznd
	- index = 1
```