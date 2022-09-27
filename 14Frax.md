

## Frax Finance



### 1. 算稳No.1

自从Terra链上的UST 和Luna 发生死亡螺旋之后，Frax 便成为了如今算法稳定币的龙头。算法稳定币是根据一套算法，来动态调整稳定币mint(铸造)出来的数量。当前Frax的生成便是靠着USDC和平台代币FXS两部分来进行合成，当FRAX 价格进行波动，场外便有了对于FRAX稳定币的套利区间，通过这种价格的锚定，最后使得稳定币FRAX稳定在1美元 。



FXS Sharas[FXS] 是FRAX 平台发行的治理代币，总的发行量为1亿枚。绝大部分的FRX代币是通过流动性挖矿进行获得的，在Uniswap 上为这三种交易对 [FRAX-USDC 33% FRAX-FXS 33% FRAX-ETH 33%]提供流动性，便可以获得Lp token， 将LP Token 在FRAX finance 平台进行质押，便会持续的挖到FXS 代币。





### 2. 锚定机制与AMO

当前USDC 占协议抵押比例的92.5%，这个抵押率还是相当的高的，说明FRAX 还是相对很稳定的，不容易发生Unpeg。

为了使FRAX 锚定在$1，当FRAX < $1的时候。拿到1枚FRAX 可以来赎回价值1美元的USDC和FXS，之后就FRX卖出，完成套利，此时抵押比例(**CR**）会升高。当FRAX> $1的时候，套利者将通过USDC和FXS去创建FRAX，并卖出FRAX而获利，此时抵押比例会降低。

在FRAX V2 中便使用AMO(Algorithmic Market Operations Controller)这套机制来自动套利，从而自己来实现FRAX的价格锚定。 FRAX 也会监控在Curve上面的FRAX 交易对，如果发生池子不平衡的状态，便会自动的将池子填补，完成价格锚定。



### 3. FPI

FPI 是一种锚定CPI的一种稳定币。随着CPI(消费者生产指数)的不断增长，1美元所能购买的东西是在下降的。当CPI 增长8%， 比如通过10000个FRAX稳定币获得同样的10000个FPI， 在CPI公布后， 我这10000枚FPI 能够兑换到10800个对应的FRAX 稳定币。
