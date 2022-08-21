# 1. Curve

Curve是什么, curve是一个专注与稳定币Swap的协议,在这里可以使用非常低的滑点来Swap对我想要的资产。因为Curve是专注与稳定币的市场， 所以在Curve做市(make market)的

3pool 是Curve上一个很经典的池子, 这三种资产是由( DAI USDC USDT )组成。当前池子这三种资产的组成比例为

- DAI     803,196,847.28   27,71%
- USDC  748,463910.83  25.82%
- USDT   1,347,192,812.21  46.47%

在池子中某个稳定币种资产的容量越大，则该币就越不被市场看好,比如当下UST 发生了与Unpeg , UST 的价格到了0.9，在当前 [ UST,[ 3pool ]]的交易对中, UST的的占比已经达到了91 %, 在4pool [UST, USDC, USDT, FRAX]中， UST 的占比也到了78.5%, 说明市场对UST 极度的不看好，大家都想用UST在池中Swap成其他更稳定的资产。

在3pool进行swap的手续费是0.03%(有一些池子是0.04%)，池子管理员要收掉这个池子手续费收益的50% ,剩下50%交易手续费分给LP(Liquidation Provider)。

池子管理员 admin 的这些管理费(50%交易手续费), 用来购买 3pool 的LPToken，—> 3CRV，同样, 3CRV也会作为veCrv holder的收益。

在做Lp的时候,既可以按照特定的比例来提供, 也可以让Curve使用钱包中最大的数量, 或者我们可以自定义提供币种的数量,来成为这个池子的LP (liquidation provider), 通过Curve的算法,拿到LP token。

把资产Deposit进入池子中,我们可以收到base APY(通过做市得到手续费的50%), 也可以收到作为LP Token。

通过Curve的公式计算, 比如我想deposit 300DAI, 250USDC, 500 USDT进入到3pool 中, 预估我就会收到1018..21个Curve 3pool Token.。

在deposit的时候, 还有一种其他选项, “deposit & stake in gauge ”，如何选了这个，这一步也就把我得到的LP token 自动的质押进了池子Curve Gauge 中, 同时,我也可以收到LP质押带来的收益。

每个池子的Curve Gauge 在总的一个Curve Gauges 会在每周通过veCRV来进行投票，获得一个对应的比例，通过这个比例，Curve会对应向每个LP池安装投票比例来分配CRV Token，而在每个Lp 池中, Curve 也会根据自己质押的LP Token的数量,  分给自己对应的 CRV Token。

在 Curve V2协议中, 开了一种新的不锚定的资产, 比如tricrpyto2, 如果在这些资产做LP, 也会像在uniswap 上面那样, 存在;一定的无常损失。

像带工厂[factory]的池子, 是非Curve 官方部署的池子, 任何人都可以在Curve部署新池，但这些池也需要审计的, 池子容量 也要 3million才能上线。

池子种类

- 普通池子 3pool
- 借贷池  compound   aave
- BTC/ETH 池    btc wbtc / eth stETH
- Factory 池

### Curve DAO

在通过提供LP 获得的CRV的过程是有一个boost过程的,  当我们把我们收益的Crv 存进入,Curve协议中,加速CRV的收益，这样可以计算到做LP 获得Crv 收益的加速值,即新的APY，最高的倍数能够达到收益的2.5倍。

加速的过程,其实也就是将我们收益的CRV进行锁仓, 对应收到 veCRV (vote&escrow )。CRV 锁仓锁的越久, 能够收益的veCRV 其实也就越多 ， 同时veCRV是不支持transfer的。

当把CRV锁进去的时候,我们的收益是:　(veCRV + 3CRV),  3CRV也可以Swap 成其他代币, 也可以直接将它提供其他包含3CRV的池子, 来做这个池的LP。

2500以上的veCRV 就可以参加CRV的投票。

项目方需要在Gauge 这里进行一个投票的竞争, 获得了更多的票数就相当于能收到更多的CRV奖励，项目方为了更多的CRV激励,便会在自己池中对用户更多的激励，提高自己的APY，很多协议在这里进行竞争， 这也就是后来著名的”Curve War ”。

持有了veCRV之后, 还可以把veCRV 存到Convex 之上, 进行质押, 获得比CRV平台更高的收益，但同时也失去了Curve中的投票权。

### Meta Pool

meta  Pool 也允许 一个Token 来与其他的 base pool(稳定的池子,比如3pool),来进行组合,  比如说当前的[ GUSD,[3pool] ]来进行组合。

这样也有助于 1. 防止污染其他池子,  降低系统风险, 这个token 比如 GUSD 归零风险

### Curve 历史

像3pool 是后来Curve上来才上的池子, Curve 最早是将资产放入到Yearn, Aave,去放贷,获得SupplyA的Apy, 这也就是之前Curve的底层资产。

### Curve的收益

- 做LP 获得50%的交易手续费(交易量越大,自己提供的LP数量越多, 收益越多)

- 基本的CRV 奖励

- 有些池会为LP提供项目方自身的代币激励(SNX,LDO)

- Stake CRV,获得veCRV来boost自己的收益率

- CRV进入Convex 获得比veCRV更高的收益

- **virtual Price**

  虚拟价格, 在Curve上做LP拿到的LP Token 会对应着一个虚拟的价格。比如在Curve 的c 池抵押 DAI/ USDC  获得cTokenLP，Curve之前会使用池中资产去Compoud 进行Supply，所以池中用cTokenLP,来换到DAI / usdc 是会有底层收益的， 所以抵押的稳定币是会逐渐增加的。