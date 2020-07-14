# lambdacli query dam

## Introduction

query dam module provides a set of subcommands to query digital asset market infos

## Usage

```
lambdacli query dam <subcommand>
```

Print all supported subcommands and flags:
```
lambdacli query dam --help
```

## Available Commands

| Name                            | Description                                                   |
| --------------------------------| --------------------------------------------------------------|
| [params](params.md)     | Query dam params |
| [markets](markets.md)   | Query all digital asset market                 |
| [market](market.md)     | Query digital asset market by asset name |
| [pool](pool.md)   | Query dam pool                |
| [miner](miner.md)   |   Query digital asset miner by address                |
| [pledge-records](pledge-records.md)   |  Query all pledge records by address                |
| [jailed-records](jailed-records.md)   |  Query all jailed records by address                |
| [refunding-records](refunding-records.md)   |  Query all refunding records by address                |
| [match-order](match-order.md)   |  Query match order by order ID               |
| [all-match-orders](all-match-orders.md)   |  Query all match orders by address              |
| [asset-match-orders](asset-match-orders.md)   |  Query all match orders related to the given asset by address               |
| [transfer-record](transfer-record.md)   |  Query transfer record and file number by order ID and receiver's address              |
| [transfer-records](transfer-records.md)   |  Query all transfer records by order ID              |
| [transfer-file-record](transfer-file-record.md)   |  Query transfer files by orderID and receiver's address             |
