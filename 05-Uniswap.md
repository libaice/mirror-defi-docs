### Uniswap & AMM



#### Uniswap是什么,应该如何使用

<img src=".\image\05-01-uniInterface.png" style="zoom:75%;" />



如图所示, 使用Uniswap 的方法非常简单，界面对于用户来说非常的友好。

只需要输入自己现有的币种，指定另外一种币种，便可以自动根据公式来进行计算自己能够获得对应币种的数量，连接上钱包之后，一笔交易便可以完成这个Token Pair 的Swap。



#### Uni Token

Uni Token 是在2020年9月份宣布发放对于之前参与过Swap 用户的空投。不过当下Uniswap Labs 并没有对Uni Token 进行更多的赋能，目前Uni 还是只要应用在进行协议的DAO投票治理上。





#### Uniswap 的迭代

**Uni-v1** 



* 可以根据这个例子[Defi-Uniswap-V1](https://jeiwan.net/posts/programming-defi-uniswap-1/)使用Solidity 来做一个Uniswap，为池子提供流动性，并试着Swap资产。

* AMM ( Auto making market )是Defi历史上的一个重要的创新，在2018年上线的uni-v1就允许Ether和另外一种Token来进行兑换。

  协议要做是建立在区块链上的去中心化交易所(DEX)。允许任何人来为交易对提供流动性。AMM 的核心逻辑就是(Constant product function) (x * y = k)。

​		x和y 分别为池中两种资产的数量，同时协议也扮演着作为价格预言机(price oracle)的作用，通过套利者([arbitrageurs](https://www.nansen.ai/research/arbitrage-on-decentralised-exchanges))来为平衡交易对的数量，从而达到价格		稳定的状态。

* Making Market : 跟根据x 与y 的比例参数，来为这个交易对提供对应的Token(ETH和另外一种Erc20代币)，此时会获得此Token Pair的LPToken。持有LP token 会根据LP 占总LP 的比例，来获得所参与此Token Pair,Swap的 0.3%手续费,。

* 如何Token Pair的创建，是由一本工厂合约来进行创建的，用户自行可以将两种Token 输入进去，来创建一个新的Token Pair。



> ​	根据公式进行化简，当输入Δ*x*的A Token的时候，会获得Δ*y*数量的 B Token

​		<img src=".\image\05-02-price_x_y.png" style="zoom:75%;" />

​	

---



**Uni-v2**

Uniswap V2 修复了用户只能使用ETH来桥接任意两种Token直接Swap的问题。可以直接创建两种ERC20 Token 在一起的Token Paire ,比如[USDC,DAI]。



Uniswap-V2 [合约源码](https://github.com/Uniswap/v2-core)



* Uniswap V2 不再支持使用ETH来做Swap,而是在用了封装的WETH来进行，这是为了满足ERC20 标准，从而实现更好的与其他ERC20 Tokens进行Swap。

​	

* [FlashSwap](https://docs.uniswap.org/protocol/V2/concepts/core-concepts/flash-swaps)
  * Flash 算是一种在存在不同价差的Dex之上进行套利，在一笔交易中，我们使用` function uniswapV2Call(address sender, uint amount0, uint amount1, bytes calldata data); `这个方法来调用FlashSwap
  * 在Uniswap上借出来950 USDC, 考虑滑点的影响与手续费，在其他Dex上，我们需要使用950+10+3 = 967 USDC 进行Swap 来得到1000 DAI。之后只需要向Uniswap 偿还967 DAI 即可完成套利(此时不考虑交易手续费)。

​	<img src="image\05-04-flashswap.png" style="zoom:73%;" />







<img src="image\05-03-v2core.jpg" style="zoom:37%;" />





**Uniswap V3**



Uni-v3 引入了新的概念，流动性区间，可以在指定的价格区间进行做市。

在引入价格区间之后，主要解决了两个问题

* 做市的集中，将之前版本的大量不用的流动性，更加专注与指定的价格区间，从而获得更多的交易手续费
* 降低无常损失的风险，发生两种资产其中一种价格暴跌的情况下，我们的损失会在价格区间进行之止损。
* 如果Token A 跌破自己的价格区间，那么我们有的LP 都会自动转换成Token B， 反之亦然。
* 要成为V3 Token Pair的LP，这时候需要我们提供一个对应的价格区间。此时LP 收到的将是一个NFT ，而非之前同质化的Erc20Token.
