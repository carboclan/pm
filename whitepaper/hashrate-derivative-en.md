
**Before [Issue](https://github.com/carboclan/pm/issues/4) is closed, please refer to Issue for most updated version**

# Tokenized Synthetic PoW Mining Contract

## 1. Motivation

Crypto mining is a sizable market. In 2018, a total of over US$ 9 billion worth of Proof-of-Work mining rewards were rewarded to miners as block rewards and transaction fees. Crypto mining often requires upfront capex investment to purchase hardware and receive certain amount of cryptocurrency as reward. There is significant risk involved in mining investment. Aside from operational risk in the construction and maintenance of mining and power facility, force majeure  events such as adverse weather condition, and policy risks, major risks associated with crypto mining are volatility in both the market price of cryptocurrencies and network mining difficulty.

There are financial instruments readily available to hedge against the market price movements of cryptocurrencies. Therefore, we will focus on risks associated with volatility in mining difficulty.

In Proof-of-Work mining, block rewards are specified by the protocol, and can be considered as fixed over a period of time. More miners joining the network will drive up the network hashrate. Difficulty is determined by a moving average targeting an average number of blocks per hour. Increased computing power would lead to increasing mining difficulty, which would reduce the economic return of mining in turn, extending the time it takes for a miner to breakeven. 

Current state of crypto mining market is inefficient. Absent of instruments to express forward-looking views without direct exposure, investors have only the choice of taking an illiquid long position via invest in mining hardware or mining operation, or choose to sit out by not investing. 

Cloud mining contracts has been in existence for many years as a proxy for non-miners to gain indirect exposure to mining cashflow, while miners can offload some of the systemic risk. However, informational asymmetry between cloud mining platforms and retail investors, as well as non-fungibility of the contracts, causing the pricing of cloud mining contracts to persistently deviate from the fundaments of the mining market. Furthermore, the lack of contract standard, opaque market structure and pervasive scams of the cloud mining contract platforms significantly hinder the formation of an efficient market. 

Market-wide informational inefficiency exacerbated with miners’ herd behavior results in wild swings in mining return as market price of cryptocurrencies moves. Miners tend to rush to market as coin price rises, driving up network difficulty which in turn results in less coins mined; as cryptocurrency prices fall, declining mining revenue may not cover the operational costs denominated in fiat, and the already illiquid mining assets becomes even harder to liquidate, leaving miners will little downside protection. 

We hereby propose Tokenized Synthetic PoW Mining Contract, which offers token holders synthetic long or short exposure to mining return, and functions similarly to mining futures by representing mining payoff. Through trading this instrument, miners can effectively hedge against risk in network difficulty, investors can be rewarded for bearing the risk. By filling in a market void via decoupling risks associated with network difficulty from that of market price of cryptocurrency, POW Mining Contract Tokens enable a more efficient mining market, and unlock possibilities of creating more crypto native financial products that service the blockchain infrastructure.

## 2. Contract Specification

The following contract is issued through [Market Protocol](https://marketprotocol.io).

###  2.1 Synthetic ETH Mining Contract

#### Index

ETH Mining Index ( _EMI_ ) represents given _N_ blocks prior to block height _H_, expected return in ETH given _Hashrate_ (Unit: Hash/s) in ethereum mining. _Difficulty<sub>i</sub>_ represents mining difficulty at block height _i_, _Coinbase<sub>i</sub>_ represents mining reward at block height _i_, and _TargetBlockTime_ represents expected block time of the ethereum network. _EMI_ is calculated as following:

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\small&space;\mathit{EMI}=\sum_{i=H-N}^{N-1}\frac{\mathit{Hashrate}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i}{\mathit{Difficulty_i}\cdot&space;2^{^{32}}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\small&space;\mathit{EMI}=\sum_{i=H-N}^{N-1}\frac{\mathit{Hashrate}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i}{\mathit{Difficulty_i}\cdot&space;2^{^{32}}}" title="\small \mathit{EHRI}=\sum_{i=H-N}^{N-1}\frac{\mathit{Hashrate} \cdot \mathit{TargetBlockTime} \cdot Coinbase_i}{\mathit{Difficulty_i}\cdot 2^{^{32}}}" /></a>

Given block height _H_, _Difficulty<sub>i</sub>_ and _Coinbase<sub>i</sub>_ are the only variables in the formula dependent on block height, all other terms are constants. Since _Coinbase<sub>i</sub>_ rarely changes, _EMI_ mostly depends on mining difficulty. _EMI_ parameters are defined as following:

Parameter | Value | Note
------| -----|-------
_Hashrate_  | 1,000,000,000,000 Hash/s  | |
_N_  | 80640  | 14-day window
_Coinbase<sub>i</sub>_  | 2 ETH per Block | Block reward is 2ETH starting from block height 7,080,000
_TargetBlockTime_ | 15 s | Target block time for ethereum is fixed at 15s

_Parameters are defined as so to maintain at least 3 significant digits to the left of the decimal, which caters to traders' heuristics in order to faciliate trading decisoins._

#### Index Cap & Floor

Each Synthetic ETH Mining Contract will specify its valid range, _Cap_ represents the upper bound, and _Floor_ represents the lower bound. When Index reaches the upper or lower bounds will trigger contract settlement.

#### Index Currency

1ETH per Index point

#### Contract Size

1ETH per Index Point

#### Expiration

Each Syntheic ETH Mining Contract will specify an expiration time, defined as ethereum block height _H_. The contract will settle when block confirmation at block height _H_ reaches _NConfirm_. For security considerations, _NComfirm_ = 960 (approximately 4 hours).

#### Settlement

At settlement, Market Protocol smart contract will send WETH to addresses that hold contract position tokens. Long token holder will receive ( _EMI_ - _Floor_ ) in WETH per Contract, short token holder will receive ( _Cap_ - _EMI_ ) in WETH per Contract.

#### Margin

Issuer of the Tokenized Synthetic Ethereum Mining Contract needs to send ( _Cap_ - _Floor_ ) amount in WETH to the Market Protocol smart contract as collateral in order to mint contract position tokens. Contract positions are fully collateralized with no need to top up margins prior to settlement.

#### Naming Convention for Contract Position Tokens

EMI-\<Floor\>-\<Cap\>-\<Height\>-[L|S]

- Floor: Index lower bound
- Cap: Index upper bound
- Height: block height for settlement
- L: long position
- S: short position

Example: EMI-100-200-80000-L token corresponds to a long position on a Synthetic Ethereum Mining Contract with Index valid range of [100,200], to be settled at block height 80,000.


###  2.2 Synthetic BTC Mining Contract
#### Index

BTC Mining Index ( _BMI_ ) represents given _2016_ blocks after block height _H_, expected return in BTC given _Hashrate_ (Unit: Hash/s) in bitcoin mining. _Difficulty<sub>i</sub>_ represents mining difficulty at block height _i_, _Coinbase<sub>i</sub>_ represents mining reward at block height _i_, and _TargetBlockTime_ represents expected block time of the bitcoin network. _BMI_ is calculated as following:

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\small&space;\mathit{BMI}=\frac{\mathit{Hashrate}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i&space;\cdot&space;2016}{\mathit{Difficulty_i}\cdot&space;2^{^{32}}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\small&space;\mathit{BMI}=\frac{\mathit{Hashrate}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i&space;\cdot&space;2016}{\mathit{Difficulty_i}\cdot&space;2^{^{32}}}" title="\small \mathit{BMI}=\frac{\mathit{Hashrate} \cdot \mathit{TargetBlockTime} \cdot Coinbase_i \cdot 2016}{\mathit{Difficulty_i}\cdot 2^{^{32}}}" /></a>

Given block height _H_, _Difficulty<sub>i</sub>_ is a variables dependent on _H_, and re-adjusts every 2,016 blocks. _Coinbase<sub>i</sub>_ is a variable dependent on _H_, which halves every 21,000 blocks. All other terms in the equation are constants. In other words, _BMI_ only depends on mining difficulty within every 2,016 blocks. Since bitcoin network adjusts difficulty every 2,016 blocks, _BMI_ remains constant until the next difficulty adjustment. _BMI_ parameters are defined as following:

Parameter | Value | Note
------| -----|-------
_Hashrate_  | 10 <sup>18</sup> Hash/s  | |
_Coinbase<sub>i</sub>_  | 12.5 BTC per Block | Block reward halves every 21,000 blocks
_TargetBlockTime_ | 600 s | Target block time for bitcoin is fixed at 10 minutes

_Parameters are defined as so to maintain at least 3 significant digits to the left of the decimal, which caters to traders' heuristics in order to faciliate trading decisoins._

#### Index Cap & Floor

Each Synthetic BTC Mining Contract will specify its valid range, _Cap_ represents the upper bound, and _Floor_ represents the lower bound. When Index reaches the upper or lower bounds will trigger contract settlement.

#### Index Currency

1BTC per Index Point

#### Contract Size

1WBTC per Index Point

#### Expiration

Each Syntheic BTC Mining Contract will specify an expiration time, defined as bitcoin block height _H_. The contract will settle when block confirmation at block height _H_ reaches _NConfirm_. For security considerations, _NComfirm_ = 24 (approximately 4 hours).

#### Settlement

At settlement, Market Protocol smart contract will send WBTC to addresses that hold contract position tokens. Long token holder will receive ( _BMI_ - _Floor_ ) in WBTC per Contract, short token holder will receive ( _Cap_ - _BMI_ ) in WBTC per Contract.

#### Margin

Issuer of the Tokenized Synthetic Ethereum Mining Contract needs to send ( _Cap_ - _Floor_ ) amount in WBTC to the Market Protocol smart contract as collateral in order to mint contract position tokens. Contract positions are fully collateralized with no need to top up margins prior to settlement.

#### Naming Convention for Contract Position Tokens

BMI-\<Floor\>-\<Cap\>-\<Height\>-[L|S]

- Floor: Index lower bound
- Cap: Index upper bound
- Height: block height for settlement
- L: long position
- S: short position

Example: BMI-100-200-80000-S token corresponds to a short position on a Synthetic BTC Mining Contract with Index valid range of [100,200], to be settled at block height 80,000.

## 3. Smart Contract Stack

Synthetic Mining Contract token issuance, trading, on-chain collateralization, and settlement are executed via smart contracts enforced by ethereum blockchain consensus. Trust is minimized in the process, which lowers the entry barrier for trading and improves liquidity.

### 3.1 Tokenization Layer

Issuers can easily issue Synthetic PoW Mining Contract by minting position tokens via [Market Protocol](https://marketprotocol.io) and traders can easily build up long or short positions by buying these position tokens, which are standard ERC20s that can be stored off-exchange in user wallets and are tradeable on both centralized and decentralized exchanges.

Contract issuers mint sets of long and short position tokens through sending collateral to Market Protocol smart contracts according to contract specifications. Once minted, contract issuers is market neutral by holding both long and short position tokens. For each contract, the outstanding long position tokens will be equal to short position tokens, as in pairs. Issuer wishing to enter into long position can sell its short position tokens, and vice versa.

Traders can buy position tokens to gain long or short exposure without becoming an issuer. Holders of position tokens can close the position and take profit any time by selling the tokens in the market without having to wait till settlement at contract expiration.

The contract specifications pre-define the cap and floor of the Index, and issuer pays full collateral according to the position ranges, there will be no liquidation prior to expiration as long as the Index falls within the ranges. However, since the Synthetic PoW Mining Contract is used to hedge against mining risk, and mining has long duration, historical volatility of difficulty must be taken into account in defining position ranges for contract specifications. 

Although contracts are fully collateralized upon issuance, the position range specification provides implicit leverage. When Index fluctuates, the rate of change in contract positions often will exceed that of the Index. The amount of leverage depends on the width of the position ranges relative to the Index, and the price of the position relative to the price range.

例1，Carboclan社区在区块链高度568512（2019-03-21）时设置了一个新的比特币挖矿算力合约。此时指数为552。设置算力收益合约的参数如下：
  - 指数上限：600
  - 指数下限：450
  - 到期时间： 区块高度574560 （约2019-05-04）

Alice希望创建0.01个合约代币对，为此她向Market智能合约质押了(600-450)*0.01=1.5WBTC，从而铸造了0.01个合约多头头寸币和0.01个合约空头头寸币。此时，按指数计算的每个合约多头代币价值为552-450=102 WBTC，每个合约空头代币价值为600-552=48 WBTC。

之后，指数下降到550，此时，按指数计算的每个合约多头代币价值为550-450=100 WBTC，每个合约空头代币价值为600-550=50 WBTC。Alice希望进入合约空头，于是她在交易所中挂单出售0.01个合约多头代币。Bob恰好希望进入合约多头，最终Bob向Alice购买了合约多头币，成交价98WBTC。Bob向Alice支付0.98WBTC，Alice向Bob支付0.01个合约多头币。

这里在市场上头寸代币成交价（98WBTC）低于了按指数计算的价格（100WBTC），这是由于人们对到期日指数会进一步下降的预期造成的。另一方面，我们可以看到，指数下降了(552-550)/552=0.36%，但多头头寸按指数计算的价格却下降了(102-100)/102=1.9%，这就是指数下限造成的5.28倍杠杆作用。

当区块高度为574570时，合约到期。又过了12个区块高度，合约进行交割。此时合约指数为525。Market智能合约向多头持有方Bob支付（525-450)*0.01=0.75WBTC, 向空头只有方Alice支付(600-525)*0.01=0.75WBTC。最终Alice的盈亏为：-1.5+0.98+0.75 = 0.23WBTC，Bob的盈亏为: -0.98+0.75=-0.23WBTC。





