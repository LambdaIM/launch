# lambdacli tx asset invest

## Description

Invest amount of asset to paticipate pre-sell stage

## Usage

```
lambdacli tx asset invest [asset] [token amount] [flags]
```

## Flags

| Name,shorthand | Type   | Required | Default               | Description                                                  |
| -------------- | ------ | -------- | --------------------- | ------------------------------------------------------------ |
| -h, --help       |        | false     |                       |  Help for asset                                        |
| --from       |        | string     |                       |  Name or address of private key with which to sign                                        |

## Examples

### pledge

```
./lambdacli tx asset invest uabc 50000000000ulamb --from val1 --broadcast-mode block
{"chain_id":"testing","account_number":"1","sequence":"0","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"lambda/MsgAssetInvest","value":{"address":"lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0","asset":"uabc","token":{"denom":"ulamb","amount":"50000000000"}}}],"memo":""}

confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'val1':
Response:
  Height: 7
  TxHash: FA8CF01D988A619AC5374B5F4B9185B73B3C7FD1FE22FC798EBD17BF60500FAD
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 38282
  Tags:
    - action = assetInvest
    - address = lambda10gat77jd5ucz7gw0m3xac8jfj5l83r6cm5ufc0
    - asset = uabc
    - fund-asset = ulamb
    - amount = 50000000000
```
