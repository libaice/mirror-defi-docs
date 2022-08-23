## ArraKis Finance 



### 1. ArraKis 是什么

ArraKis 协议建立在Uniswap v3上面，目的就是为了管理用户作为LP的收益，使用一些做市策略，将Make market 的收益进行优化，从而达到流动性管理的服务。

目前协议支持了Ethereum, Optimsim 和Polygon 三条链。

当前Uniswap 面临的一些问题

* Uniswap V2使用AMM模型，当价格波动只在某个区间时，资金的利用效率就会很低。
* Uniswap 使用了流动性区间的方式来进行做市，但这样却增加了LP的风险和复杂性。

ArraKis 做了流动性的管理，当前在uniswapV3的LP 也已经达到了19%，成为Uniswap 的最大的LP。



### 2. 如何使用协议

ArraKis ,(原名G-Uni)，[这篇文章](https://medium.com/gelato-network/introducing-g-uni-lp-like-a-pro-in-uniswap-v3-8fd6fdf9fc35)讲述了GUNI当时产品的一些特性与要解决的一些问题。

GUNI结合了Uni-V3的资金利用效率和UniV2的简单实用性，用户可以直接像在uni-V2 上面那样为Token Pair 提供流动性，成为LP。

* 自动复投LP收到的手续费奖励，成为一种复利的收益
* 管理流动性的做市范围，使得当前资金的做市区间一直在市场中有效的价格区间
* 在用户在Uniswap V3做市后，获得到Uniswap V3的Token凭证，这个凭证将会直接被deposit成为GUNI的LP， 之后同样管理这些Pairs的做市区间。

* 协议通过[Gelato](gelato.network)来作为价格监控的方案，当价格变动时，Gelato便会提醒G-NUI 触发做市的流动区间，调整价格。