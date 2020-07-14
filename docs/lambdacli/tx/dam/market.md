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

# lambdacli tx dam market authorize

## Introduction

Authorize mining public key for a specific digital asset market

## Usage

```
lambdacli tx dam market authorize [asset] [flags]
```

- `asset`: market related to this asset

Print help messages:
```
lambdacli tx dam market authorize --help
```

## Unique Flags

| Name, shorthand     | type   | Required | Default  | Description                                                         |
| --------------------| -----  | -------- | -------- | ------------------------------------------------------------------- |
| --from | string | true     | ""       |  Name or address of private key with which to sign |
| --pubkey | string | true     | ""       |  key path to load pubkey to authorize digital asset mining |

## Examples

```
lambdacli tx dam market authorize uabc --from master --pubkey ../pubkey.json
```

pubkey.json
```
{
  "pub_key": {
    "type": "tendermint/PubKeyEd25519",
    "value": "Pyd/mJPIdBhtUDNerCZORLPv5Ovjf8/ujlNA+X5tMgE="
  }
}
```

Output:

```
Response:
  Height: 182
  TxHash: B2AF9FDB7BBAEBEAEA72CA30129397D199AE8753CD880A81B312EE85AE4A4540
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 18360
  Tags:
    - action = authorizeMiningPubKey
    - address = lambda105jf3p5qkrnq973xmc6e9f8asly79sv7phcrym
```

