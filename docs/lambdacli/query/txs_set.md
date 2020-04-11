## bank  

| Name | Type    | Description                                                  |
| -------------- | --------------------- | ------------------------------------------------------------ |
| MsgSend       |   send     |       转账交易                           |
| MsgMultiSend       |  multisend      |     未使用            |

## distribution

| Name | Type    | Description                                                  |
| -------------- | --------------------- | ------------------------------------------------------------ |
| MsgWithdrawMinerRewards       |   withdraw_miner_rewards     |       提取存储挖矿收益                           |
| MsgWithdrawDelegatorReward       |  withdraw_delegator_reward      |     提取收益            |
| MsgModifyWithdrawAddress       |  set_withdraw_address      |     设置提现地址            |
| MsgWithdrawValidatorCommission       |  withdraw_validator_rewards_all      |     共识节点提取佣金收益            |

## gov

| Name | Type    | Description                                                  |
| -------------- | --------------------- | ------------------------------------------------------------ |
| MsgDeposit       |   deposit     |       存入押金                           |
| MsgSubmitProposal       |  submit_proposal      |     发起提案            |
| MsgVote       |  vote      |     投票            |

## slashing

| Name | Type    | Description                                                  |
| -------------- | --------------------- | ------------------------------------------------------------ |
| MsgUnjail       |   unjail     |       validator 解禁                           |
| MsgUnjailPartner       |   unjail_partner     |       节点合伙人 解禁                           |

## staking

| Name | Type    | Description                                                  |
| -------------- | --------------------- | ------------------------------------------------------------ |
| MsgCreateValidator       |   create_validator     |        创建节点                           |
| MsgEditValidator       |   edit_validator     |       编辑节点                        |
| MsgDelegate       |   delegate     |       节点质押                          |
| MsgBeginRedelegate       |   begin_redelegate     |       节点转质押                          |
| MsgUndelegate       |   begin_unbonding     |       节点反质押                          |


## asset

| Name | Type    | Description                                                  |
| -------------- | --------------------- | ------------------------------------------------------------ |
| MsgAssetPledge       |   assetPledge     |        兑换资产                           |
| MsgAssetDrop       |   assetDrop     |       兑换Token                        |
| MsgCreateAsset       |   createAsset     |       创建资产                          |
| MsgMintAsset       |   mintAsset     |       增发资产                          |
| MsgLockAsset       |   lockAsset     |       锁定资产                          |
| MsgUnLockAsset       |   unLockAsset     |       解锁资产                          |
| MsgDestroyAsset       |   destroyAsset     |       销毁资产                          |
| MsgRuinAsset       |   ruinAsset     |       毁灭资产                          |

## market

| Name | Type    | Description                                                  |
| -------------- | --------------------- | ------------------------------------------------------------ |
| MsgCreateMarket       |   createMarket     |        创建市场                           |
| MsgEditMarket       |   editMarket     |       修改市场参数                        |
| MsgWithDrawMarket       |   withdrawMarket     |       提取市场收益                          |
| MsgCreateMiner       |   createMiner     |       创建矿工                          |
| MsgEditMiner       |   editMiner     |       修改矿工                          |
| MsgCreateSellOrder       |   createSellOrder     |       创建卖单                          |
| MsgCancelSellOrder       |   cancelOrder     |       取消卖单                          |
| MsgCreateBuyOrder       |   createBuyOrder     |       创建买单                          |
| MsgMinerWithDraw       |   minerWithdraw     |       矿工赔付金和订单收入提现                          |
| MsgMinerWithDrawCount       |   minerWithdrawCount     |       矿工赔付金和订单收入批量提现                          |
| MsgMaintain       |   maintain     |       矿工维护                          |
| MsgUnMaintain       |   unmaintain     |       矿工解除维护                          |
| MsgUnjailMiner       |   unjailMiner     |       矿工解除监禁                          |
| MsgOrderRenewal       |   orderRenewal     |       用户续费                          |

## pdp

| Name | Type    | Description                                                  |
| -------------- | --------------------- | ------------------------------------------------------------ |
| MsgStatement       |   statement     |        提交挖矿声明                           |
| MsgPDPProofs       |   pdpProofs     |       提交挖矿证明                        |

