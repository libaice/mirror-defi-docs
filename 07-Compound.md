### 7.Compound 



### 1.Compound 是什么

在金融市场上，一个很重要的问题就是资产利用效率的问题。比如我当前持有A资产，但此时此刻，我需要B 资产的流动性，但我此刻依然相信A资产的未来会增值的预期。

在Defi 领域能够使用合约的方式来很好的解决这一问题。

在2020年，DefiSummer前夕，Compound 通过激励Comp Token ， 开启了流动性挖矿的阶段。Compound 简单来说，是一种借贷协议，用户通过超额抵押的方式，来借出来一定比例的代币，从而增加了资产使用率。



### 2.Compound 的运作公式

当前我有了一定数量的A资产，当前想要将我此时此刻的A资产Supply进入协议中，调用CErc20合约中的mint 方法，同时参数传入自己想要mint 进去的Token 的数量，协议会根据当前市场的exchangeRate 来将此传入数量数量的Token， 转换为对应数量(根据公式计算， cTokenAmt = tokenAmt * exchangeRate )。 

某个市场如果有借款，随着借款量越大，借款人对此市场的exchangeRate 的提升就会越高。资产的有效利用率也就对应的变得更高。

调用`borrow`方法，便可以在自己资产状况足够健康的情况下，借出来一定量的B Token。

如果发生了B 资产的价格不断上涨，或者A 资产的价格不断下跌，当自己的借出来的比例达到了清算线，其他用户便可以将自己所持资产进行清算。



### 3. Comp Token 

Compound是引爆了"流动性挖矿"的概念。通过call Comptroller 合约中`_setCompSpeed ` 的方法，设置整个池中释放Comp Token 的速率，每个市场中也单独有个`compRate`方法，来调整这个市场的释放的速率。



comp Token 是一本标准的ERC20 合约，comp Holder 可以对Compound 协议参与治理。社区可以参与提案，投票。持有100个Comp token 便可以参与对提案的投票治理，持有25000个Comp 可以参与提案的发起。



### 4.Oracle 喂价

池中所有资产的价格，通过chainLink 来进行报价。Chainlink 可以通过单独的ValidatorProxy 合约，来为每个cToken 进行报价，每个validatorProxy 都是唯一的，这些合约都是链上唯一的。





### 5.清算

当用户的所有借款量大于其最多可以借出金额的数量的时候，用户便会进入清算列表。此时，清算人可以偿还借款人的债务，同时可以获得借款人所抵押的资产。并且可以拿到另外8%（清算激励）的抵押资产。

