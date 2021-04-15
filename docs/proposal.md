# 社区提案教程

### 提案相关说明
参考：[Lambda社区治理](http://docs.lambda.im/governance/)

### 查询社区账户
``` 
./lambdacli query distr community-pool
```

### 发起社区提案
发起社区提案：
```shell script
./lambdacli tx gov submit-proposal community-pool-spend community.json --from [account] --broadcast-mode block -y 
```

创建community.json文件（`vi community.json`），内容如下：
``` 
{
  "title": "Community Pool Spend",
  "description": "Community Pool Spend",
  "recipient": "lambda1thj5fv8d0dsh3aealhpxm9mvgxjfh87s224esr",
  "amount": [
    {
      "denom": "ulamb",
      "amount": "10000"
    }
  ],
  "deposit": [
    {
      "denom": "ulamb",
      "amount": "10000000"
    }
  ]
}
```
- `recipient`为接收金额地址  
- `amount`下`amount`为接收金额  
- `deposit`下`amount`为存入提案金额，存入金额满10000LAMB后提案会进入投票阶段，提案投票成功后该金额返还到原账户   

### 存入押金（deposit）
提案发起成功后，tx结果会返回proposal-id，或者通过`./lambdacli query gov proposals`查找自己提交的提案proposal-id

存款：
``` 
lambdacli tx gov deposit [proposal-id] [deposit-amount]ulamb --from [account]
```


### 投票（vote）
节点和矿工账户可进行投票，可重复投票覆盖之前的投票结果
``` 
./lambdacli tx gov vote [proposal-id] [option] --from [account]
```
`option`可填写为yes/no/no_with_veto/abstain



