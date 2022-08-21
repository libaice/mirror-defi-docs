### Convex Finance 



#### What is Convex

在Curve协议上面提供流动性，会获得LP Token, Curve DAO使用CRV Token来激励这些LPs。

CRV当前在Curve上面的主要用途有

* 参与Curve的治理
* lock CRV to acquire veCRV(non-transferable)  用户可以使用veCRV来参与投票与托管(vote &escrow)
* 使用CRV来Boost自己的收益 APY, 加速收益率



如果在Curve的进行做市，拿到的LP Token 只能参与Liquidity Gauge(决定CRV向每个LP池的分配比例)。

可是如果在Curve上面用CRV来boost 收益的话，每次操作自己的仓位，都会导致boost 比例的改变，这个boost比例跟池子大小，和CRV币价，和自己所在池中的所站比例都会有影响。而且每次操作, 在Ethereum网络拥堵的状况下，都会发生交易手续费过高的情况。



这时候就有了收益聚合平台，比如 Yearn，在Yearn上面质押自己的LP, Yearn 将这些LP获得的CRV奖励，换成LP Token，持续增加本金。



这个时候Curve自家也出了一个新的平台，Convex，Convex会保留我们所收益的CRV Token。



而在新的Convex平台，收到本身的CRV奖励外，还有有CVX 治理Token的激励,所以收益是分成两部分的,vAPR(variable APR), v代表 variable 的意义，这个v 和用户deposit 资产的数量，用户lpToken 所在的交易对的交易量，资产价格都有相关性。



* Curve LP APR  收益Curve上面的交易手续费(50%分给LP)
* boost CRV 收益 比如下面 收益



<img src="image\06-01-convexapy.png" style="zoom:75%;" />





#### How to use Convex

​	

* 质押Curve上做市的Lp Tokens

  直接将Curve 中的LP 来放到Convex 上面，获取收益。

  

* 在Convex 平台质押CRV

  如果将CRV在Curve平台进行质押，将会获得veCRV, veCRV 可以参与投票治理，并获得平台50%的手续费分红。

  在Convex质押CRV，需要将手中的CRV 先转化成cvxCRV，虽然丢失了veCRV的投票治理功能，但增加了Convex 增强的CRV收益。

  cvxCRV是支持transfer的，但是不支持转回CRV,但可以在二级市场进行交易swap兑换成CRV。

  

* 获得的cvxCRV可以再次被质押到Convex平台上，从而获得CVX 的Token激励

  > Convert CRV to cvxCRV. By staking cvxCRV, you’re earning the usual rewards from veCRV 
  >
  > * 3crv governance fee distribution from Curve 
  > *  any airdrop
  > * plus a share of 10% of the Convex LPs’ boosted CRV earnings
  > *  and CVX tokens on top of that.

* 质押CVX 来获得cvxCRV的收益

  获得的cvxCRV之后，可以在次质押进人Convex 协议中，从而获取更多的CVX，手续费，加速apr 的收益。




![](.\image\06-02-cvxcrv.png)



* **锁仓CVX(lock CVX)**

  如果之前将收益的CVX已经质押到Convex上去挖cvxCRV，会有当下的收益(现在2.44%)，其实还有另外的选择: 既将手中的CVX进行锁仓。会获得一个比直接活期质押更高的收益率。
  
  不过锁仓期默认就是16weeks。这需要更长时间，不能操作自己进行锁仓的资产。

​	