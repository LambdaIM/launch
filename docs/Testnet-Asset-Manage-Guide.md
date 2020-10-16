# 资产管理

## 资产角色

1. 资产创建者: 创建该资产的人，同时只有创建人可以创建对应的资产市场
2. 预挖矿参与者: 预挖矿阶段的参与者，在预挖矿阶段质押LAMB/TBB，待资产发行后可以获取对应数额的发行资产
3. 资产持有者: 账户内拥有该资产的人

## 资产说明

1. 资产以token的形式存储在Lambda链上。
2. 任意Lambda账户都可以创建资产, 创建资产需要消耗一定量的LAMB(100万)。资产最大发行量为900亿。
3. 预挖矿结束后，创建资产的账户地址拥有该资产的初始总量，可以对该资产进行增发和毁灭。
4. 参与预挖矿的参与者在预挖矿阶段结束后可以获得一定额度的资产，根据投入的锚定资产比例来获取。
5. 资产持有人可以进行资产转账、锁定、解锁、销毁，所有交易需要消耗LAMB作为手续费。
6. 毁灭资产会返还创建时消耗的90%的LAMB到原账户(即返还90万LAMB)。
7. 在资产创建者创建对应的资产市场后，可以在市场内质押资产来获取资产分账(仅限增发类型资产)

## 创建资产

创建资产需要消耗账户的1000000LAMB(1LAMB=1000000ulamb)

```
./lambdacli tx asset create [amount+asset] [amount+ulamb] \
--asset-name [asset-name] --mint-type [mint-type] --total-supply [total-supply] \
--inflation [inflation-amount] --adjust-rate [adjust-rate] --adjust-period [adjust-period] --max-adjust-count [max-adjust-count] \
--genesis-height [genesis-height] --mining-ratio [mining-ratio] \
--fund-asset [amount+fund-asset] --fund-stake [amount+asset] \
--fund-period [fund-period] --from [account-name]
```

- `[amount+asset]`: 想要创建的资产和创建人初始资产数额，在预挖矿阶段完成后，这部分资产会转入创建者账户，资产必须以`u`开头，不可以包含`tbb`,`lamb`和`1amb`等；
- `[amount+ulamb]`: 创建资产需要的手续费，当前默认为1000000000000ulamb（=100w LAMB）；
- `[asset-name]`: 资产的名称，例如`XBB Coin`
- `[mint-type]`: 资产的类型，当前有三种 not_mint/one_time_mint/inflated_mint
  - `not_mint`: 不增发类型，资产在发行后不可以增发
  - `one_time_mint`: 一次性增发类型，可使用增发命令`lambdacli tx asset mint`每次增发指定数额资产
  - `inflated_mint`: 线性增发类型，在增发命令激活以后会根据资产创建时候配置的属性来进行增发
- `[total-supply]`: 资产的最大总量，不能超过90000000000000000(=900亿)
- `[fund-asset]`: 预挖矿的期望投资资产类型和数额，当前可以为`ulamb`和`utbb`
- `[fund-stake]`: 预挖矿结束后返回的资产类型和数额，资产类型和创建的资产类型必须一致
- `[fund-period]`: 预挖矿周期，单位为天，可填写范围为3～120天，预挖矿结束的标志为 已经达到预挖矿的投资额度 或 已到预挖矿周期时间。

***注意***

这里需要注意，预挖矿周期到达后，如果没有达到预期的投资金额，则只给参与的参与者返回对应的资产金额，未达到部分资产不发行，如果没有参与者，则所有预挖矿资产直接在发行后转到资产创建者的账户

- `[account]`: 创建者的账户

以下的`flag`在非`inflated_mint`类型中不用指定

- `[inflation]`: 线性增发每块增发的数量(初始)
- `[adjust-rate]`: 每次调整衰减增发的比例
- `[adjust-period]`: 每次多少块进行增发调整
- `[max-adjust-count]`: 资产一共可以进行几次调整
- `[genesis-height]`: 增发开始块高必须高于这个块高
- `[mining-ratio]`: 资产挖矿奖励占增发奖励的比例

例如：
```
创建inflated_mint类型uxxb资产（账户余额要保证有100w LAMB，用于创建资产），
创建人账户预留1亿 XXB（=100000000000000uxxb, 1XXB=1000000uxxb）资产，
预挖矿周期30天（fund-period），预挖矿投资额度100000 LAMB（fund-asset），预挖矿结束后按投资比例返还10000000XXB（fund-stake）到投资账户。

指定从第50000块高（genesis-height）开始挖矿增发（50000块高以前不增发），
每块增发1000000uxxb（inflation），增发10000块（adjust-period）后，
根据减产系数（adjust-rate）调整每块增发数量为500000uxxb（=1000000uxxb * 0.5），按此数量再增发10000块，
以此类推，第二次调整增发数量为250000uxxb，第三次调整增发数量为125000uxxb，第四次调整增发数量为62500uxxb，
到第五次（max-adjust-count）调整增发数量为31250uxxb后，不再调整增发数量，每块按31250uxxb增发直到总资产数量达到发行资产总量（total-supply）900亿XXB

./lambdacli tx asset create 100000000000000uxxb 1000000000000ulamb \
--asset-name "XBB Coin" \
--mint-type inflated_mint \
--total-supply 90000000000000000 \
--inflation 1000000 \
--adjust-rate 0.5 \
--adjust-period 10000 \
--max-adjust-count 5 \
--genesis-height 50000 \
--fund-asset 100000000000ulamb \
--fund-stake 10000000000000uxxb \
--fund-period 30 \
--from mykey
```
[创建数字资产](lambdacli/tx/asset/create.md)

## 资产预挖矿

资产发行有个预挖矿阶段，参与者可以投资某种锚定的资产来参与，在预挖矿结束后，可以获取对应的发行资产。

```
./lambdacli tx asset invest [asset] [amount+fund] \
--from [account-name]
```

- `[asset]`: 指定参与某个正在预挖矿阶段的资产
- `[amount+fund]`: 投资的锚定资产和金额

在资产预挖矿阶段结束后，会根据投资的比例获取对应金额的发行资产，可以多次发起增加投资金额，这里返回的金额必须为整数位，所以用户在投资时候尽量根据比例来进行投资

```
例如

资产类型 uxxb
预挖矿数量为 300000000uxxb
期望投资资产和金额为 100000000ulamb

则投资比例为
100000000:300000000 = 1:3
即每投入1ulamb，可获得3uxxb

比如用户test投资1LAMB，预挖矿结束后按比例可获得3XXB
./lambdacli tx asset invest uabc 1000000ulamb --from test

用户在投资时候尽量投资10的整数倍来进行，如果不是10的整数倍，可能会导致小数部分的资产无法获取
```
[参与预挖矿](lambdacli/tx/asset/invest.md)

用户可以通过接口进行查询

```
./lambdacli query asset fund-info [asset] [address]
```

- `[asset]`: 发行资产
- `[address]`: 参与者地址

[查询预挖矿结果](lambdacli/query/asset/fund-info.md)

## 资产增发

增发类型的资产(`one_time_mint`/`inflated_mint`)可以通过命令进行增发或者增发激活，只有资产的创建人可以发起此类交易

```
lambdacli tx asset mint [amount+symbol]
```

- `[amount+symbol]`: 增发的资产类型和金额，`one_time_mint`类型的资产是一次性增发，`inflated_mint`类型的资产在发起后相当于是激活增发，会根据创建时候的增发属性来进行增发
[资产增发](lambdacli/tx/asset/mint.md)
