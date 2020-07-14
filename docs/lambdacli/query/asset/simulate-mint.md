# lambdacli query asset simulate-mint

## Introduction

Simulate an asset mint period

## Usage

```
lambdacli query asset simulate-mint [flag]
```

## Flags

| Name,shorthand  | Type    | Required  | Default  | Description                                             |
| :-------------- | :------ | :-------- | :------- | :------------------------------------------------------ |
| -h, --help      |         |  false    |          |  Help for asset                                         |
| --asset         | string  |  true     |          | asset reserved amount                                   |
| --total-supply  | int     |  true     |          | total supply is upper limit of asset supply             |
| --inflation     | int     |  true     |          | the asset's initial inflation per height                |
| --adjust-rate   | double  |  true     |          | the adjust rate about inflation                         |
| --adjust-period | int     |  true     |          | adjust inflation when period reached                    |
| --max-adjust-count | int  |  true     |          | if reached max adjust count, it won't adjust inflation anymore |
| --genesis-height| int     |  true     |          | produce asset only if reached genesis height            |


## Examples

```
./lambdacli query asset simulate-mint \
--asset 10000000uxxb \
--total-supply 100000000 \
--inflation 1000 \
--adjust-rate 0.5 \
--adjust-period 10000 \
--max-adjust-count 5 \
--genesis-height 5

startHeight:5         endHeight:10004     inflation:1000
startHeight:10005     endHeight:20004     inflation:500
startHeight:20005     endHeight:30004     inflation:250
startHeight:30005     endHeight:40004     inflation:125
startHeight:40005     endHeight:50004     inflation:62
startHeight:50005     endHeight:2328391   inflation:31
startHeight:2328392   endHeight:2328392   inflation:3

```


