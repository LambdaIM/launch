# lambdacli tx dam market create

## Introduction

Create a digital asset market

## Usage

```
lambdacli tx dam market create [market-name] [asset] [exchange-ratio] [flags]
```

- `market-name`: name of the digital asset market
- `asset`: market related to this asset
- `exchange-ratio`: exchange ratio from uxxb to utbb

Print help messages:
```
lambdacli tx dam market create --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx dam market create test-market uabc 100
```

Output:

```
Response:
  Height: 47
  TxHash: 355150AA7D1368F957620B43266BA5B3AE1445093DA2AA4995CC67AB0F745BD5
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 34027
  Tags:
    - action = createDigitalAssetMarket
    - address = lambda105jf3p5qkrnq973xmc6e9f8asly79sv7phcrym
    - asset = uabc
```

# lambdacli tx dam market dismiss

## Introduction

Dismiss a existing digital asset market

## Usage

```
lambdacli tx dam market dismiss [asset] [flags]
```

- `asset`: which asset digital market to dismiss

Print help messages:
```
lambdacli tx dam market dismis --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx dam market dismiss uabc --from master
```

Output:

```
Response:
  Height: 95
  TxHash: 3157EACEC74DA8A91BC77D0A18BBF2F6291D4C508BF37F4C8752C574A794083E
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 26157
  Tags:
    - action = dismissDigitalAssetMarket
    - address = lambda105jf3p5qkrnq973xmc6e9f8asly79sv7phcrym
```

# lambdacli tx dam market authorize-user

## Introduction

Authorize a user is allowed to buy order in a specific digital asset market

## Usage

```
lambdacli tx dam market authorize-user [asset] [userAddr] [flags]
```

- `asset`: market related to this asset
- `userAddr`: authorized user's address

Print help messages:
```
lambdacli tx dam market authorize-user --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx dam market authorize-user uabc lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel
```


Output:

```
Response:
  Height: 17047
  TxHash: AC790CEDB74759141366B586B8152EA625B3BB6027ABBB6D0244898C4C70C48B
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 12895
  Tags:
    - action = authorizeUser
    - address = lambda105jf3p5qkrnq973xmc6e9f8asly79sv7phcrym
    - user = lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel
    - asset = uabc
    - isAllowed = true
```

# lambdacli tx dam market forbid-user

## Introduction

Forbid a user from buying order in a specific digital asset market

## Usage

```
lambdacli tx dam market forbid-user [asset] [userAddr] [flags]
```

- `asset`: market related to this asset
- `userAddr`: authorized user's address

Print help messages:
```
lambdacli tx dam market forbid-user --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |

## Examples

```
lambdacli tx dam market forbid-user uabc lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel
```


Output:

```
Response:
  Height: 17081
  TxHash: EE4A13D86849E0679A0BA84ADC02293383518E2ACB65994E90C46F8D8403835D
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 11791
  Tags:
    - action = authorizeUser
    - address = lambda105jf3p5qkrnq973xmc6e9f8asly79sv7phcrym
    - user = lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel
    - asset = uabc
    - isAllowed = false
```

