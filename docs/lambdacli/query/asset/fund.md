# lambdacli query asset fund

## Introduction

Querying commands for the asset module fund info by symbol

## Usage

```
lambdacli query asset fund [asset] [flags]
```

## Examples

### Query asset lock from address

```
./lambdacli query asset fund uabc
AssetFundInfo:
  Asset:     10000000000uabc
  FundAsset: 100000000000ulamb
  Status:    funded
  Amount:    100000000000
  EndTime:   2020-09-09 10:03:58.987544 +0000 UTC
```


