# lambdacli query pool match-order

## Description

Query the pool match orders by order ID

## Usage
```
 lambdacli query pool match-order [orderID] [flags]
```

Print help messages:
```
lambdacli query pool match-order -h
```

## Examples

Query the pool match order
```
lambdacli query pool match-order 324FA8BEC7822E1A636B62CE5094AEA6B449AF6E
```

```
MatchOrder
  OrderId:               324FA8BEC7822E1A636B62CE5094AEA6B449AF6E
  AskAddress:            lambdamineroper16dmwfy5fg5t2fcyekmu7r2q350avdpwqm3usvz
  BuyAddress:            lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel
  SellOrderId:
  BuyOrderId:
  Price:                 0
  Size:                  100
  CreateTime:            2021-01-22 03:28:06.684767 +0000 UTC
  EndTime:               2021-02-21 03:28:06.684767 +0000 UTC
  CancelTimeDuration:    0s
  WithDrawTime:          2021-01-22 03:28:06.684767 +0000 UTC
  Status:                0
  MarketAddress:         lambdamarketoper1yl9v25pcxem9e5g828f84d9xu97h4qx5p667tp
  UserPay:               0ulamb
  MinerPay:              0ulamb
  PeerId:
  DhtId:                 FP7YvNKxonBThX2RCip4eZNtRMi9mwVXeiE3MCVH1WMd
```
