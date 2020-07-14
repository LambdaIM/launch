# lambdacli tx asset create

## Description

lambda asset create, the symbol prefix must be 'u', the token amount must be 1000,000LAMB(1000,000,000,000ulamb)

## Usage

```
lambdacli tx asset create [amount+symbol] [amount+token] [flag]
```

## Flags

| Name,shorthand  | Type    | Required  | Default  | Description                                             |
| :-------------- | :------ | :-------- | :------- | :------------------------------------------------------ |
| -h, --help      |         |  false    |          |  Help for asset                                         |
| --asset-name    | string  |  false    |          |  Asset Full Name                                        |
| --mint-type     | string  |  true     |          |  Asset mint type, options: not_mint/one_time_mint/inflated_mint  |
| --total-supply  | int     |  false    |   0      |  Only for `inflated_mint` type, total supply is upper limit of asset supply |
| --inflation     | int     |  false    |   0      | Only for `inflated_mint` type, the asset's initial inflation per height |
| --adjust-rate   | double  |  false    |   0      | Only for `inflated_mint` type, the adjust rate about inflation |
| --adjust-period | int     |  false    |   0      | Only for `inflated_mint` type, adjust inflation when period reached |
| --max-adjust-count | int  |  false    |   0      | Only for `inflated_mint` type, if reached max adjust count, it won't adjust inflation anymore |
| --genesis-height| int     |  false    |   0      | Only for `inflated_mint` type, produce asset only if reached genesis height|
| --from          | string  |  true     |          |  Name or address of private key with which to sign      |

## Examples
```
$ ./lambdacli tx asset create 1000uxxb %sulamb \
--asset-name "XBB Coin" \
--mint-type inflated_mint \
--total-supply 100000000000000 \
--inflation 1000000 \
--adjust-rate 0.5 \
--adjust-period 10000 \
--max-adjust-count 5 \
--genesis-height 10000 \
--from lambda17am6rkcsm6sguy57rwr5fpkuezp620wfxsgkzn --broadcast-mode block -y

Password to sign with 'lambda-001':
Response:
  Height: 12358
  TxHash: 2F17114965B74F60585A1BF58D85B09A3D7C8859B285FA8A96C8790104C25BEA
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 49520
  Tags: 
    - action = createAsset
    - address = lambda17am6rkcsm6sguy57rwr5fpkuezp620wfxsgkzn
    - name = XBB Coin
    - symbol = uxxb
    - amount = 1000
```
