# lambdacli tx

## Introduction

tx module provides a set of subcommands to send、staking、slashing、asset、gov、sign transactions.

## Usage

```
lambdacli tx <subcommand>
```

Print all supported subcommands and flags:
```
lambdacli tx --help
```

## Available Commands

| Name                            | Description                                                   |
| --------------------------------| --------------------------------------------------------------|
| [send](send.md)       | Create and sign a send tx                                             |
| [sign](sign.md)     | Sign transactions generated offline                                      |
| [multisign](multisign.md)     | Generate multisig signatures for transactions generated offline     |
| [broadcast](broadcast.md)   | Broadcast transactions generated offline                 |
| [encode](encode.md)   | Encode transactions generated offline                 |
| [distr](./distr/README.md)             | Distribution transactions subcommands                                     |
| [staking](./staking/README.md)   | Staking transaction subcommands                                           |
| [slashing](./slashing/unjail.md)                   | Slashing transactions subcommands                                           |
| [asset](asset/README.md)                             |  Asset transactions subcommands                                            |
| [gov](./gov/README.md)                        |  Gov transactions subcommands
| [market](market/README.md)                             |  market transactions subcommands                                            |
