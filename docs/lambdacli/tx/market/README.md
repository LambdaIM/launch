# lambdacli market

## Introduction

market module provides a set of subcommands to send market transactions.

## Usage

```
lambdacli tx market <subcommand>
```

Print all supported subcommands and flags:
```
lambdacli tx market --help
```

## Available Commands

| Name                            | Description                                                   |
| --------------------------------| --------------------------------------------------------------|
| [create-market](create-market.md)                       | Create new market actor                                |
| [edit-market](edit-market.md)                       | edit market actor                                |
| [withdraw-market](withdraw-market.md)                           | withdraw market income                                                           |
| [create-miner](create-miner.md)                           | create miner actor                                                         |
| [edit-miner](edit-miner.md)                                       | edit miner info                                                       |
| [create-sellorder](create-sellorder.md)                                   | create a sell order by miner                                      |
| [cancel-order](cancel-order.md)                                   | cancel a sell order by miner                                      |
| [create-buyorder](create-buyorder.md)                                   | create a buy order by user                                     |
| [withdraw-miner](withdraw-miner.md)                                   | withdraw a match order reward                                     |
| [miner-withdraw-count](miner-withdraw-count.md)                                   | withdraw miner orders                                      |
| [maintain](maintain.md)                                   | maintain a miner                                      |
| [unmaintain](unmaintain.md)                                   | cancel maintain miner                                      |
| [unjail](unjail.md)                                   | free a miner                                      |
| [order-renewal](order-renewal.md)                                   | renew a match order                                      |


