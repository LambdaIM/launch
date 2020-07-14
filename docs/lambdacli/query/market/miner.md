# lambdacli query market miner

## Description

Query miner info

## Usage
```
 lambdacli query market miner [address] [flags]
```

Print help messages:
```
lambdacli query market miner -h
```

## Examples

Query miner info by address
```
lambdacli query market miner lambda1h29mncmlezu2jsrsyvsg7vmd9zq8nt75mmqffw
```

### Description

|  Field    | Description  |
| --------- | ------------ | 
|  Status     | 0 Available, 1 Maintaining, 2 Jailed   |  


```
Miner
  Operator Address:           lambdamineroper1h29mncmlezu2jsrsyvsg7vmd9zq8nt7505vwun
  Status:                     0
  AllSize:                    1000.000000000000000000
  UsedSize:                    400.000000000000000000
  MatchSize:                  0.000000000000000000
  DhtId:                      8Et9kcTMpixkfggqPqWcd4XaYWgQNwF7WCNdbPF18YFZ
  PeerId:                     
  OrderPledge:                2000000000ulamb
  OrderReward:                0ulamb
  LastWithDrawTime:           1970-01-01 00:00:00 +0000 UTC
  MiningAddress:              lambda1urudd7phn2chstjz9sm6hk2q9hq6c2e4zguwju
  MissedPDPChallenge:         0
```
