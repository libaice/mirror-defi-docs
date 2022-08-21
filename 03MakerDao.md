## MakerDao



#### DAI的基本逻辑

在经历了Terra 这波之后, MakerDao 现在已经是Tvl最高的Defi项目了。

Maker同样也是很早的Defi项目了, 算是算法稳定币的始祖项目了。

其核心的金融逻辑就自己手中的ETH进行超额抵押, 从而铸造算法稳定币DAI , 增加资金的流动性和利用效率，DAI锚定美元的一种资产。



如果发生ETH暴跌的情况, 那么将会将抵押的ETH进行清算/拍卖。

如果想要取回自己所抵押的资产的时候，则需要额外偿付一笔(Satability Fee)稳定费, 此时系统会销毁自己所偿还的DAI，从而取回自己所抵押的资产。



如果自己的资产超过了清算线, 那么自己的资产则会被拍卖，拍卖者会轮流出价，拍价最高者会胜出。

清算人(liquidator) 帮我们偿还超借的DAI资产，并且获得此时抵押的抵押品(ETH/WBTC),并且有一笔清算收益(13%左右)。



MakerDAO协议同样发行了另外一种代币 : MKR， MKR主要用来治理，通过DAO的方式来生成提案，MKR Holders可以用MKR来进行投票参与治理。

提案内容有:(Stablity Fee)稳定费率, The DSR(Dai Saving Rate), 债务上线等等。



债务拍卖: 当MakerDao的系统出现大量的财政赤字, 协议将增发MKR,并且将DAI进行拍卖来进行资本的重组。





#### 如何操作

1. **Borrow**
   * 既可以将资产直接deposit 进去,也可以将资产deposit 和generate Dai 放在同一笔交易中
   * 正常情况下偿还DAI的时候，需要repay额外一部分的 DAI来作为稳定费 Stability Fee
2. **Multiply**
   * minimum Vault Debt 开一个vault 最少需要借出来的DAI 数量， 既抵押的资产必须达到一定数量，才能开 multiply 仓位。
   * 允许用户在使用抵押品借入 DAI 的同时，创建高达 4 倍的杠杆头寸。其中这些头寸类似于杠杆或保证金头寸，但用户无需从中心化的交易对手那里借款，只需将抵押品存入金库，以抵押生成的 DAI 作为购买更多抵押品的资金来源，从而实现杠杆效果。





**抵押资产类型**

这里列举的是几种较为热门的抵押的资产，ETH-B 类型是风险最高的，借出了同样多的DAI在发生ETH价格暴跌的时候，也是最可能先被清算的，并且这种类型需偿还的利息也是最高的。

使用CRVv1-ETHSTETH-A 这种LP Token来进行抵押，首先将自己的ETH资产质押到Lido 协议中，得到stETH，stETH是一种不断生息的Token，此时用stETH在Curve上进行做市，此时可以拿到交易手续费,CRV激励(if stake CRV, then boost Crv APY), LDO Token 奖励, 并且获得Crvv1stETH 这种LPToken 。

此时再使用LP Token 来Maker进行抵押，在清算线之下可以借出来DAI, 不断的套娃。

原来Defi 就是一场不断让资本利用效率增加的游戏。



| ETH-Type                                            | 抵押率/清算线 | (Stability Fee） | 风险 |
| --------------------------------------------------- | ------------- | ---------------- | ---- |
| ETH-A                                               | 145%          | 2.25%            | 中等 |
| ETH-B                                               | 130%          | 4%               | 最高 |
| ETH-C                                               | 170%          | 0.5%             | 最低 |
| WstETH-A                                            | 160%          | 2.25%            | 中等 |
| CRVV1STHSTETH-A<br />(LP of Curve pool [ETH,stETH]) | 155%          | 2.25%            | 中等 |

同样其他池的资产也有

* BTC [ WBTC-A  , WBTC-B, WBTC-C, RenBTC-A ]

* UniLP [ UniV2-DAI-ETH-LP-A,   UniV2WBTCETH-A, UNIV2USDCETH-A, UNIV2DAIUSDC-A  , UNIV2UNIETH-A, UNIV2WBTCDAI-A]

* Link Mana GUSD Curve LP 等等..





### DAI 拍卖的流程细节

https://daiauctions.com/

**抵押品拍卖参数**

* 每批规模 (50 -> 500ETH )
* 每次竞价时长( 10min -> 6h)

* 最小竞价增幅  3%
* 最长竞价周期  3days



**完成的拍卖流程**

​	场景: 用户在ETH 为$180的时候参与抵押1Ether，借出了100 DAI，此时清算价格为 180 / 150% = $120

​	当价格触及150%的时候触发清算线，如果此时发生ETH价格的暴跌，Ether当前价格为 $120

​	120 / 150% = 80，此时对用户的抵押资产1Eth 来进行竞拍

​	清算罚金 13%  需要回购的DAI 数量 ( 100 + 100 * 13% = ) 113 DAI

* 竞价过程

  		1.  清算人A参与竞价,   使用50 DAI 来要到用户的1eth,  此时系统会赤字(63 DAI)

  2. 清算人B参与竞拍,  使用 113 DAI 来获得用户的1ETH， 此时系统不会赤字，清算人B 有7$的利润

     此时系统已经安全

* 反向拍卖
  	    3. 清算人C 竞价113DAI 来拍用户抵押品的99% 既0.99 ETH = 118.8$

​		  4.  清算人D 竞价113 DAI 来拍用户的98 %  既0.98 ETH = 117.6$  此时还能获得 4.6$的收益。



数据含义(同样ID 一条)

* Kick 启动拍卖

  * lot  抵押资产	

  * bid 拍价
  * 当时价格

* Tend 竞价

* DENT 反向拍卖

* TAKE 拍卖成功， 查看用户竞拍的详情数据



### DAI当前数据看板

https://daistats.com/#/overview

* Debt Ceiling 当前总抵押资产课借出的DAI 的总量(天花板)
* DAI 总发行量