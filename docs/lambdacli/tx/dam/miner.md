# lambdacli lambdacli tx dam miner pledge

## Introduction

Pledge amount of asset to acquire mining size

## Usage

```
lambdacli tx dam miner pledge [asset] [size] [flags]
```

- `asset`: which asset to pledge
- `size`: size to pledge, unit is a module parameter(default GB)

Print help messages:
```
lambdacli tx dam miner pledge --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |
| --order-price | string | true     | ""       |   set order price, unit is uxxx/GB/month |

## Examples

```
lambdacli tx dam miner pledge uabc 1000GB --order-price 3000000uabc --from master
```

Output:

```
Response:
  Height: 499
  TxHash: 9168926F87BE6990C84F46FEE50E45EA9D8AEBC60FA8660DD86609E0E395F376
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 31462
  Tags:
    - action = digitalAssetPledge
    - address = lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
    - asset = uabc
    - cost = 10000000
```

# lambdacli tx dam minenr refund

## Introduction

Refund pledged asset 

## Usage

```
lambdacli tx dam miner refund [asset] [flags]
```

- `asset`: which asset to refund

Print help messages:
```
lambdacli tx dam miner refund --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx dam miner refund uabc
```

Output:

```
Response:
  Height: 6780
  TxHash: 2FD19442DBCBA6F343F7098CDA1B53C491929E0ADC6849C6175CE978CB47D5EA
  Data: 0101
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 68922
  Tags:
    - action = digitalAssetRefund
    - address = lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
    - asset = uabc
    - amount = 10000000
```

# lambdacli tx dam miner activate

## Introduction

Activate a digital asset miner if deactivated for lack of sufficient pdp proofs

## Usage
```
lambdacli tx dam miner activate [asset] [flags]
```

- `asset`: which asset miner to activate

Print help messages:
```
lambdacli tx dam miner activate --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx tx dam miner activate uabc --from master
```

Output:

```
Response:
  Height: 6900
  TxHash: 2FD19442DBCBA6F343F7098CDA1B53C491929E0ADC6849C6175CE978CB47D5EA
  Data: 0101
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 68922
  Tags:
    - action = activateMiner
    - sender = lambda1mn7dvaa45mzfefq52antavyvfjluvsgl3v3pyw
```

# lambdacli tx dam miner deactivate

## Introduction

Deactivate a digital asset miner by validator for lack of submitting pdp proof on time

## Usage
```
lambdacli tx dam miner deactivate [asset] [minerAddr] [flags]
```

- `asset`: asset digital market
- `minerAddr`: which asset miner to deactivate by a valid validator

Print help messages:
```
lambdacli tx dam miner deactivate --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx dam miner deactivate uabc lambda105jf3p5qkrnq973xmc6e9f8asly79sv7phcrym --from validator
```

Output:

```
Response:
  Height: 7000
  TxHash: 2FD19442DBCBA6F343F7098CDA1B53C491929E0ADC6849C6175CE978CB47D5EA
  Data: 0101
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 68922
  Tags:
    - action = deactivateMiner
    - sender = lambda1mn7dvaa45mzfefq52antavyvfjluvsgl3v3pyw
	- miner = lambda105jf3p5qkrnq973xmc6e9f8asly79sv7phcrym
    - asset = uabc
	- rewarded = 100
	- burned = 100
```

# lambdacli tx dam miner withdraw

## Introduction

Withdraw match order's reward by order ID

## Usage
```
lambdacli tx dam miner withdraw [matchOrder-id] [flags]
```

- `matchOrder-id`: order ID of the match order

Print help messages:
```
lambdacli tx dam miner withdraw --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx dam miner withdraw 65F21496016CDF70F165E32FB9FC43B5B19B87CA --from master
```

Output:

```
Response:
  Height: 5088
  TxHash: 0A7C6AD9D7EC63DD92E13885A2CAD1E54C0D5F465013704365E448E6C0B6D209
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 38499
  Tags:
    - action = damMinerWithdraw
    - address = lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
    - matchOrderID = 65F21496016CDF70F165E32FB9FC43B5B19B87CA
    - withdrawMiner = 10000000uabc
```

# lambdacli tx dam miner withdraw-count

## Introduction

Withdraw a range of match order's reward by address and asset

## Usage
```
lambdacli tx dam miner withdraw-count [asset] [page] [limit] [flags]
```

- `asset`: match orders related to this asset
- `page`: page of match orders
- `limit`: max match orders per page


Print help messages:
```
lambdacli tx dam miner withdraw-count --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
./lambdacli tx dam miner withdraw-count uabc 1 10 --from master
```

Output:

```
Response:
  Height: 5144
  TxHash: 2D0D5EA2A152C1389B7856CAB79777E86025628614A27C9CDC97877293FFD475
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 39614
  Tags:
    - action = damMinerWithdrawCount
    - address = lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
    - withdrawMiner = 100000uabc
    - allCount = 1
    - withDrawCount = 1
    - withDrawIdList = 65F21496016CDF70F165E32FB9FC43B5B19B87CA
    - withDrawDetail = 0a3b0a28363546323134393630313643444637304631363545333246423946433433423542313942383743411204756162631a090a0475616263120130
    - withdrawTime = 2020-07-02 08:57:05.01151 +0000 UTC
```