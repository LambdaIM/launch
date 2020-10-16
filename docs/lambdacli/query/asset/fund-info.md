# lambdacli query asset fund-info

## Introduction

Querying commands for the asset module fund stake info by symbol and funder's address

## Usage

```
lambdacli query asset fund-info [asset] [address] [flags]
```

## Examples

### Query asset lock from address

```
./lambdacli query asset fund-info uabc lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
AssetFundStakeInfo:
  Funder: lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
  Invest: 50000000000ulamb
  Stake:  5000000000uabc
```


