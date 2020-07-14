# lambdacli query market sequence

## Description

Query the sequence symbol key

## Usage
```
lambdacli query market sequence [marketAddress] [flags]
```

Print help messages:
```
lambdacli query market sequence -h
```

## Examples
First, get marketAddress with `lambdacli query market markets `
```
Market
  marketAddress:        lambdamarketoper1thj5fv8d0dsh3aealhpxm9mvgxjfh87srk3887
  name:                 LambdaMarket
  owner:                lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr
  profit:               lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr
  feeRate:              0.020000000000000000
  commissionRate:       0.020000000000000000
  inCome:
      feeInCome:        411894050000ulamb
      commissionInCome: 526144000000ulamb
  payMent:              46420727500000ulamb

```

And then, query the sequence symbol key with marketAddress
```
./lambdacli query market sequence lambdamarketoper1thj5fv8d0dsh3aealhpxm9mvgxjfh87srk3887 -o json --indent
```

```
{
  "cursor": "A5FE65BFA2ED2FB163181E8B341345BA4179CCE5",
  "size": "4",
  "list": [
    {
      "key": "A5FE65BFA2ED2FB163181E8B341345BA4179CCE5",
      "value": [
        "544C6D171A118A0C262C7A91E398E0CCF8343022",
        "EF4588686BCA4F46806998F0320332B39082C3E8"
      ]
    },
    {
      "key": "EF4588686BCA4F46806998F0320332B39082C3E8",
      "value": [
        "A5FE65BFA2ED2FB163181E8B341345BA4179CCE5",
        "D868ED486E36FEAE1F7CD92AA44AEF222D63112C"
      ]
    },
    {
      "key": "D868ED486E36FEAE1F7CD92AA44AEF222D63112C",
      "value": [
        "EF4588686BCA4F46806998F0320332B39082C3E8",
        "544C6D171A118A0C262C7A91E398E0CCF8343022"
      ]
    },
    {
      "key": "544C6D171A118A0C262C7A91E398E0CCF8343022",
      "value": [
        "D868ED486E36FEAE1F7CD92AA44AEF222D63112C",
        "A5FE65BFA2ED2FB163181E8B341345BA4179CCE5"
      ]
    }
  ]
}
```
