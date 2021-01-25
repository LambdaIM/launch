# lambdacli query

## Introduction

query module provides a set of subcommands to query block tx validator.

## Usage

```
lambdacli query <subcommand>
```

Print all supported subcommands and flags:
```
lambdacli query --help
```

## Available Commands

| Name                            | Description                                                   |
| --------------------------------| --------------------------------------------------------------|
| [tendermint-validator-set](tendermint-validator-set.md)     | Get the full tendermint validator set at given height                                     |
| [block](block.md)     | Get verified data for a the block at given height                                     |
| [txs](txs.md)     | Search for paginated transactions that match a set of tags     |
| [tx](tx.md)   | Find a transaction by hash in a committed block                 |
| [account](account.md)   | Query account balance                 |
| [info](info.md)   | query the information of upgrade module                 |
| [distr](./distr/README.md)   |  Querying commands for the distribution module                |
| [staking](./staking/README.md)   |  Querying commands for the staking module                                          |
| [minting](./minting/README.md)   |  Querying commands for the minting module                                         |
| [slashing](./slashing/README.md)                   | Querying commands for the slashing module                                           |
| [asset](asset/README.md)                             |  Querying commands for the asset module                                            |
| [gov](./gov/README.md)                             |  Querying commands for the gov module                                            |
| [market](market/README.md)                             |  Querying commands for the market module                                            |
| [dam](dam/README.md)                             |  Querying commands for the dam module                                            |
| [pool](pool/README.md)                             |  Querying commands for the pool module                                            |

