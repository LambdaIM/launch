# lambdacli query asset all-fund-infos

## Introduction

Querying commands for the asset module all fund stake info by symbol

## Usage

```
lambdacli query asset all-fund-infos [asset] [flags]
```

## Examples

### Query asset lock from address

```
./lambdacli query asset all-fund-infos uabc
AssetFundStakeInfo:
  Funder: lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
  Invest: 50000000000ulamb
  Stake:  5000000000uabc
AssetFundStakeInfo:
  Funder: lambda17mzpym4zvtmlk8ulcrw77k5ty3jjcjupsuka89
  Invest: 50000000000ulamb
  Stake:  5000000000uabc
```


