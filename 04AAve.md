### Aave



#### Aave是什么

Aave可以算是目前在Tvl排行中最大的借贷协议了。目前已经在Ethereum,polygon,Avalance,Arbitrum , Fantom, Harmony等链上部署了协议。

协议也已经从开始的v1迭代到了现在的v3版本。



传统市场场上的抵押逻辑是: 我现在有一套房，目前还在住着，可是现在生活上面出现了意外，急需大量的现金流(假设我的房产价格大于所需现金流)，那么此时我就可以将自己的这套房产抵押到银行，从而借出来这一部分现金流。

如果在我使用现金流的这期间，我的房子发生升值，我依然在偿还完银行的贷款和利息之后，获得我原有的房产所属权。



把这套逻辑放在Defi 应用中，假如此刻我持有Ether，同时我看好ETH的未来，可现在我需要一笔其他币种来用于其他地方。此时Aave就是一个非常好的选择。在不损失我原有资产的情况下，增加了我当前手中资产的流动性。



目前Aave-v3版本已经上了Arbitrum/OPtimism/Polygon 等等这些layer2或二层网络，但是在Ethereum layer1主网还没有上线，所以在Ethereum主网上面使用的依然是Aave-v2协议。



在这张表格中可以看到当前以太主网上的各种数据。

https://docs.google.com/spreadsheets/d/1TY_ai7vapncY66HUdkFp8G8W7owIQOS2lqTsdvqm6PY/edit#gid=0





#### AAve使用

这个协议操作起来也是方便的:

目前很多协议使用了 **thegraph**来作为数据的索引，比如当前[Aave v2](https://thegraph.com/explorer/subgraph?id=CvvUWXNtn8A5zVAtM8ob3JGq8kQS8BLrzL6WJV7FrHRy&view=Overview) 就在上面做了Subgraph，使用web端Dapp的时候，直接使用GraphQL 来进行查询区块链的状态，协议数据以及用户的数据。 

* Asset To Supply

  * 直接使用Supply 按钮,可以将自己钱包中的资产供应到池子中
  * 资产Supply进入池中，会将我们的资产按照1:1的关系自动转换到aToken分给自己。

  * aToken是自动按照Apy (Rebaseable)进行复利增长的，想要withdraw 自己supply进资产的时候，可以换到等同于aToken数量的资产。
  * Reward APR 从reserve储备金中会分出一部分的stkAAVE用户额外的收益，stkAAVE为用户质押Aave获得的LpToken。

* Asset to borrow

  * 可变与恒定APY : 可变的利率是根据当下市场的供需关系来决定的，而恒定的则比较固定，不会根据市场变化而变化。
  * borrow  资产的时候, 会借出这种资产和债务, 债务资产为分为 aStableDebtToken/ aVariableDebtToken。两种资产都是不可transfer的。

*  Health Factor
  * 健康系数，抵押品 总价值* 清算线 / 借出品总价值  ，如果系数< 1 触发清算机制。
  * LTV (loan to value) 当前所借出资产总价值占了可借出总价值的比例。  超过清算线, 则会触发清算机制。



* Stake AAVE
  * 直接将Aave代币进行质押，获得 stkAAVE 质押LPtoken
  * 冷却期  10天, 不能取回自己所质押的资产
  * AAVE/ETH BPT 是 使用aave & ETH token pair 在Balancer 进行做市获得的LP，在这里进行质押获得AAve收益。
  * Max Slashing 如果出现整个系统的财政赤字，将最多使用30%用户质押的资产来弥补赤字来保护协议。 

​	

*  Liquidations
  * 目前协议使用机器人liquidatorBot 来检测( health factor <1 ) 的用户，这些用户可以被清算
  * 最多偿还50% 的债务，清算过程会得到一笔 加上清算激励的用户抵押资产。
  * 如果用户资产多类型抵押，则可以选择清算激励更高的资产来进行清算。



<img src="D:\dapp\mirror\image\04-01supplyDAI.png" style="zoom:60%;" />



#### goverance

使用aave / stkAAVE 可以在snapshot上为aave 协议的proposal 进行投票，从而参与AAve 社区的治理。

 

<img src="D:\dapp\mirror\image\04-02-aaveSnapshot.png" style="zoom:60%;" />



#### Aave闪电贷

Flash Loan 运作在不开启抵押的时候，在同一比交易中，借入大量的资产，并偿还对应的利息

目前Aave Flash loan 的对每笔闪电贷首先0.09% 的手续费。

如果这这笔交易不能够=偿还对应借出的资产，那么这笔交易则执行失败。



https://github.com/Aave/flashloan-box



一些闪电贷的应用

* https://collateralswap.com/
  * 比如在MakerDao上面抵押ETH 借入DAI，发生ETH价格暴跌的情况，可以在一笔交易内将抵押品换到借出资产，从而减少用户的损失

* defisaver.com
  * 一站式来管理自己账号中的Defi应用。

https://docs.aave.com/faq/flash-loans