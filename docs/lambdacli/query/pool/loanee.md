# lambdacli query pool loanee

## Description

Query loanee by address

## Usage
```
 lambdacli query pool loanee [address] [flags]
```

Print help messages:
```
lambdacli query pool loanee -h
```

## Examples

Query the loanee
```
lambdacli query pool loanee lambda16dmwfy5fg5t2fcyekmu7r2q350avdpwq07shel
```

After that, you will get loanee in chain

```
Loanee:
  address:    lambdamineroper16dmwfy5fg5t2fcyekmu7r2q350avdpwqm3usvz
  rewards:
    Loanee Reward
  marketAddress:        lambdamarketoper1yl9v25pcxem9e5g828f84d9xu97h4qx5p667tp
  totalReward:          0.000000000000000000ulamb
  oneDayReward:         0.000000000000000000ulamb
  withDrawable:         0.000000000000000000ulamb
  averageOneDayReward:  0.000000000000000000ulamb
```
