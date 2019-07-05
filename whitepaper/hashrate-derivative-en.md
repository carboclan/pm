**Before [Issue](https://github.com/carboclan/pm/issues/4) is closed, please refer to Issue for most updated version**

# Tokenized Synthetic PoW Mining Contract

## 1. Motivation

Crypto mining is a sizable market. In 2018, a total of over US$ 9 billion worth of Proof-of-Work mining rewards were rewarded to miners as block rewards and transaction fees. Crypto mining often requires upfront capex investment to purchase hardware and receive certain amount of cryptocurrency as reward. There is significant risk involved in mining investment. Aside from operational risk in the construction and maintenance of mining and power facility, adverse weather condition and policy risks, there are two major risks associated with crypto mining: market price of cryptocurrencies and network mining difficulty.

There are financial instruments readily available to hedge against the market price movements of cryptocurrencies. Therefore, we will focus on risk associated with volatility in mining difficulty.

In Proof-of-Work mining, block rewards are specified by the protocol, and can be considered as fixed over a period of time. More miners joining the network will drive up the network hashrate. Difficulty is determined by a moving average targeting an average number of blocks per hour. Increase in computing power would drive up mining difficulty, which would in turn reduce the economic return of mining. 

Current state of crypto mining market is inefficient. Absent of instruments to express forward-looking views without direct exposure, investors have only the choice of taking an illiquid long position via invest in mining hardware or mining operation, or choose to sit out by not investing. 

Miners sometimes resort to selling "cloud mining" contracts as an imperfect hedge against both difficulty and price movements. Typical cloud mining contracts require investors to pay to the issuer (cloud mining platform or a miner) in full upfront and receive a stream of cashflow over an indefinite period of time. It is a proxy for non-miners to gain indirect exposure to mining cashflow, while miners can offload some of the systematic risks. However, this instrument subjects investors to significant counterparty risks, and has been hotbed for scams.

Lack of effective instrument leave miners unhedged in the wild swings in mining return. Miners tend to rush to market as coin price rises, driving up network difficulty which in turn results in less coins mined; as cryptocurrency prices fall, declining mining revenue may not cover the operational costs denominated in fiat, and the already illiquid mining assets becomes even harder to liquidate, leaving miners with little downside protection. 

We hereby propose Tokenized Synthetic PoW Mining Contract, which offers token holders synthetic exposure to mining payoff. Through trading this instrument, miners can hedge against difficulty, investors can be rewarded for bearing the risk. By filling in a market void via decoupling risks associated with network difficulty from that of market price of cryptocurrency, POW Mining Contract Tokens enable a more efficient mining market, and unlock possibilities of creating more crypto-native financial products that service the blockchain infrastructure.

## 2. Contract Specification

The following contract is issued through [Market Protocol](https://marketprotocol.io).

###  2.1 Synthetic ETH Mining Contract

#### Index

ETH Mining Index ( _EMI_ ) represents expected return (ETH) per unit _Hashrate_ (Hash/s) at given _N_ blocks prior to block height _H_ in ethereum mining. _Difficulty<sub>i</sub>_ represents mining difficulty at block height _i_, _Coinbase<sub>i</sub>_ represents mining reward at block height _i_, and _TargetBlockTime_ represents expected block time of the ethereum network. _EMI_ is calculated as following:

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\small&space;\mathit{EMI}=\sum_{i=H-N}^{N-1}\frac{\mathit{Hashrate}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i}{\mathit{Difficulty_i}\cdot&space;2^{^{32}}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\small&space;\mathit{EMI}=\sum_{i=H-N}^{N-1}\frac{\mathit{Hashrate}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i}{\mathit{Difficulty_i}\cdot&space;2^{^{32}}}" title="\small \mathit{EHRI}=\sum_{i=H-N}^{N-1}\frac{\mathit{Hashrate} \cdot \mathit{TargetBlockTime} \cdot Coinbase_i}{\mathit{Difficulty_i}\cdot 2^{^{32}}}" /></a>

Block height _H_, _Difficulty<sub>i</sub>_ and _Coinbase<sub>i</sub>_ are the only variables in the formula dependent on block height. All other terms are constants. Since _Coinbase<sub>i</sub>_ rarely changes, _EMI_ mostly depends on mining difficulty. _EMI_ parameters are defined as following:

Parameter | Value | Note
------| -----|-------
_Hashrate_  | 1,000,000,000,000 Hash/s  | |
_N_  | 80640  | 14-day window
_Coinbase<sub>i</sub>_  | 2 ETH per Block | Block reward is 2ETH starting from block height 7,080,000
_TargetBlockTime_ | 15 s | Target block time for ethereum is fixed at 15s

_Parameters are defined as so to maintain at least 3 significant digits to the left of the decimal, which caters to traders' heuristics in order to facilitate trading decisions._

#### Index Cap & Floor

Each Synthetic ETH Mining Contract will specify its valid range, _Cap_ represents the upper bound, and _Floor_ represents the lower bound. Index reaching the upper or lower bound prior to expiration will trigger contract settlement.

#### Index Currency

1ETH per Index point

#### Contract Size

1ETH per Index Point

#### Expiration

Each Synthetic ETH Mining Contract will specify an expiration time, defined as ethereum block height _H_. The contract will settle when block confirmation at block height _H_ reaches _NConfirm_. For security considerations, _NComfirm_ = 960 (approximately 4 hours).

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
 
BTC Mining Index ( _BMI_ ) represents expected return (BTC) per unit _Hashrate_ (Hash/s) at given _2016_ blocks after block height _H_ in bitcoin mining. _Difficulty<sub>i</sub>_ represents mining difficulty at block height _i_, _Coinbase<sub>i</sub>_ represents mining reward at block height _i_, and _TargetBlockTime_ represents expected block time of the bitcoin network. _BMI_ is calculated as following:

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\small&space;\mathit{BMI}=\frac{\mathit{Hashrate}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i&space;\cdot&space;2016}{\mathit{Difficulty_i}\cdot&space;2^{^{32}}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\small&space;\mathit{BMI}=\frac{\mathit{Hashrate}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i&space;\cdot&space;2016}{\mathit{Difficulty_i}\cdot&space;2^{^{32}}}" title="\small \mathit{BMI}=\frac{\mathit{Hashrate} \cdot \mathit{TargetBlockTime} \cdot Coinbase_i \cdot 2016}{\mathit{Difficulty_i}\cdot 2^{^{32}}}" /></a>

Given block height _H_, _Difficulty<sub>i</sub>_ is a variable dependent on _H_, and re-adjusts every 2,016 blocks. _Coinbase<sub>i</sub>_ is a variable dependent on _H_, which halves every 21,000 blocks. All other terms in the equation are constants. In other words, _BMI_ only depends on mining difficulty within every 2,016 blocks. Since bitcoin network adjusts difficulty every 2,016 blocks, _BMI_  remains constant until the next difficulty adjustment. _BMI_ parameters are defined as following:

Parameter | Value | Note
------| -----|-------
_Hashrate_  | 10 <sup>18</sup> Hash/s  | |
_Coinbase<sub>i</sub>_  | 12.5 BTC per Block | Block reward halves every 21,000 blocks
_TargetBlockTime_ | 600 s | Target block time for bitcoin is fixed at 10 minutes

_Parameters are defined as so to maintain at least 3 significant digits to the left of the decimal, which caters to traders' heuristics in order to facilitate trading decisions._

#### Index Cap & Floor

Each Synthetic BTC Mining Contract will specify its valid range, _Cap_ represents the upper bound, and _Floor_ represents the lower bound. Index reaching the upper or lower bound prior to expiration will trigger contract settlement.

#### Index Currency

1BTC per Index Point

#### Contract Size

1WBTC per Index Point

#### Expiration

Each Synthetic BTC Mining Contract will specify an expiration time, defined as bitcoin block height _H_. The contract will settle when block confirmation at block height _H_ reaches _NConfirm_. For security considerations, _NComfirm_ = 24 (approximately 4 hours).

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

Synthetic PoW Mining Contract token issuance, trading, on-chain collateralization, and settlement are executed via smart contracts enforced by ethereum blockchain consensus. Trust is minimized in the process, which lowers the entry barrier for trading and improves liquidity.

### 3.1 Tokenization Layer

Issuers can easily issue Synthetic PoW Mining Contract by minting position tokens via [Market Protocol](https://marketprotocol.io) and traders can easily build up long or short positions by buying these position tokens, which are standard ERC20s that can be stored off-exchange in user wallets and are tradeable on both centralized and decentralized exchanges.

Contract issuers mint sets of long and short position tokens pairs by sending collateral to Market Protocol smart contracts according to contract specifications. Once minted, contract issuers is market neutral by holding both long and short position tokens. For each contract, the outstanding long position tokens will be equal to short position tokens, as in pairs. Issuer wishing to enter into long position can sell its short position tokens, and vice versa.

Traders can buy position tokens to gain long or short exposure without becoming an issuer. Holders of position tokens can close the position and take profit any time by selling the tokens in the market without having to wait till settlement at contract expiration.

The contract specifications pre-define the cap and floor of the Index, and issuer pays full collateral according to the position ranges, there will be no liquidation prior to expiration as long as the Index falls within the ranges. To provide effective hedges for actual mining, miners would prefer not to face arbitrary liquidation prior to expiration. Position ranges in contract specifications must be defined wide enough to cover volatility in difficulty. 

Although contracts are fully collateralized upon issuance, the position range specification provides implicit leverage. When Index fluctuates, the rate of change in contract positions often will exceed that of the Index. The amount of leverage depends on the width of the position ranges relative to the Index, and the price of the position relative to the price range.

Example 1. The Index is at 552 now, Carboclan Community specifies a new Synthetic BTC Mining Contract at block height 568512 (2019-03-21). The contract specifications are as follow: 
  - Cap: 600
  - Floor: 450
  - Expiration: block height 574560 (expected date 2019-05-04)

Alice would like to mint 0.01 units of contract position token pair. She sends (600-450) * 0.01=1.5WBTC to the Market smart contract as collateral, and minted 0.01 long position token and 0.01 short position token. A long token is worth 552-450=102 WBTC, a short token is worth 600-552=48 WBTC.

Later on, the Index falls to 550, a long token is worth 550-450=100 WBTC, a short token is worth 600 - 550 = 50 WBTC. Alice would like to enter into a short position, so she lists her 0.01 long position in the market. Bob would like to enter into a long position, so he bought the 0.01 long position token, at a price of 0.98WBTC. Bob paid to Alice 0.98WBTC and received 0.01 long token.

While the actual price of the position token may be above or below the Index, in this example actual price of the long position token (98WBTC) may be priced below the theoretical price (100WBTC) calculated from the current Index, which may be caused by market expectation that the Index may drop further by expiration. On the other hand, while Index drops (552-550)/552=0.36%, but theoretical price for the long position token calculated from the Index drops (102-100)/102=1.9%, which reflects 5.28 implicit leverage from the Index floor.

The contract expires at block height 574570, and settles after 12 blocks. The Index is at 525. Market Protocol smart contract pays Bob (525-450) * 0.01=0.75WBTC, and (600-525) * 0.01=0.75WBTC to short position token owner Alice. Alice's return: -1.5+0.98+0.75 = 0.23WBTC，Bob's return: -0.98+0.75=-0.23WBTC。

### 3.2 Oracle
Market Protocol relies on oracle to provide Index for settlement. Oracle is the relatively centralized part of the entire system.
Calculating EMI for the Synthetic ETH Mining Contract does not require off-chain data. Difficulty data can be obtained directly from smart contract. The major challenge is that a single call cannot access the difficulty data for the entire 80640 blocks. Difficulty data needs to be stored on the smart contract continuously.

Calculating BMI requires off-chain data. Bitcoin mining difficulty data needs to be obtained from third party provider. The difficulty data is then processed by the oracle smart contract. The good news is that bitcoin mining difficulty only change every 14 days on average. Since the difficulty data is recorded on the bitcoin chain, all people can validate the authenticity of the data.

### 3.3 Trading Layer

Since the position tokens issued by Market Protocol are fully collateralized and fit ERC-20 standard, the position tokens can be traded on any centralized exchange (i.e. Binance and Bitstamp), and decentralized exchanges (i.e. 0x and Uniswap). Thus, tokenized Synthetic PoW Mining Contract is readily tradeable without having to develop new infrastructure or technology.

### 3.4 Variable Margin Layer

In 3.1 we’ve already analyzed the implicit leverage of the Market Protocol. However, when the Index fluctuate significantly, in order for the index not to touch the cap and floor, the Index range need to be set wider, which leads to a higher collateral ratio and lower leverage.

Short-term mining contracts (i.e 30 days) have less fluctuation. Therefore, the Index range is narrow and Market Protocol itself enables enough implicit leverage. However, long-term mining contracts (i.e 180 days) could fluctuate more than 100%, the fully collateralized method of Market Protocol will be capital inefficient.

Therefore, a variable margin layer could be introduced on top of the position token. The variable margin layer has such characteristic that a certain margin ratio is set according to the market price of the position. Margins only need to cover fluctuation in the short run and cannot cover the entire position. When the margin ratio drops due to market price change, margin calls can be issued to the party lacking margin so as to cover the fluctuation. On the other hand, if the margin ratio increases to more than necessary, the excess margin can be withdrawn from the margin account to pocket the profit. Such a variable margin system lowers the margin requirement and increase capital efficiency.

A few DeFi protocols (i.e. dydx) can enable variable margin function. User can borrow token from dydx. Lender can deposit token A to the token pool of the smart contract. Borrower mortgages token B to create margin account and borrow token A from the token pool. The token A he borrowed is sold for token B. The token B he bought is again mortgaged into the margin account so that he can borrow more token A to be sold. The leveraged short on token A is now complete. 

On the contrary, lender could deposit Token B to the token pool of the smart contract. Borrower mortgage Token A to create margin account and borrow Token B from the token pool. The Token B he borrowed is sold for Token A. Token A he bought is again mortgaged into the margin account so that he can borrow more Token B to be sold for Token A. The leveraged long on Token A is now complete.

Dydx supports a maximum leverage of 4x. When the price of the mortgaged token drops relative to the borrowed token, margin could drop to an insufficient amount. If the borrower cannot add enough collateral in time, forced liquidation could occur. Variable margin is thus functional.

At the moment, dydx does not fully support position tokens from market protocol, more integration work still needs to be done.

## 4. Use Cases

Tokenized Synthetic PoW Mining Contract has multiple use cases.

### 4.1 Risk Exposure

Before purchasing mining rigs and start mining, investors need to estimate ROI. Purchasing mining rigs is a onetime investment. Electricity cost for mining is fixed as well. Therefore, investment for mining is fixed. The only factors affecting mining output is price movement and mining difficulty. Various financial product (futures, perpetual swaps and options) can hedge against price fluctuation. Synthetic POW Mining Contract fills the market void by revealing risks associated with difficulty fluctuation. Investors could observe the market price for mining contract of various durations, which reflects market view on mining return.

i.e On May 1st, 2019, BMI index is 526. The following table indicates the market price for Tokenized Synthetic PoW Mining Contracts in various terms.

Contract position token |	Expiration date |	Market price	| Implied mining return
------|-----|-------|----- 
BMI-450-600-574560-L | 19-05-04 |	75  | 525
BMI-450-600-576576-L | 19-05-18	| 65	| 515
BMI-450-600-578592-L | 19-05-31	| 50	| 500
BMI-450-600-580608-L | 19-06-14	| 35	| 485

Long position token prices reflect market view on mining returns of respective difficulty cycles. The market believes that under same amount of hashrate, the mining return will gradually decrease. To be specific, the amount of bitcoin that could be mined with 10^18 hash/s of hashrate within next 2016 blocks (1 difficulty cycle). Investors could figure out that expected mining return gradually decreases, thereby estimating their own mining ROI more rationally.

### 4.2 Hedging
The synthetic POW mining contract can hedge mining risks in addition to revealing them. Similarly, we set aside the cryptocurrency price movement here, since many derivatives can hedge that. Investors could enter a short position in said contract to hedge difficulty related risks when mining. When difficulty goes up, mining return goes down, the profit on the short position could negate the decrease in actual mining return. When difficulty goes down, mining return goes up, the loss on the short position could negate the increase in actual mining return. The hedging process thus locked in mining return. The return is (cap of the index - the price when entering the position)

For example, on May 1st, 2019, Alice purchased a batch of mining rigs that clocks 10^17 hash/s. She wanted to lock in mining return for nearly the next two months from block height 574,560 (05-04) to block height 582,624 (06-28). Therefore, Alice purchased a series of short positions of the mining contracts in chronological order, 0.1 token each. The following table reflects her P&L.

Position Token	| Expiry date	| Entry Price	| Index when settled	| Position P&L 	| Mining income	| Comprehensive income
------|-----|------- | ----- |----|----|----
BMI-450-600-574560-S	| 05-04	| 75	| 525.3	| -0.03	  | 52.53	| 52.50
BMI-450-600-576576-S	| 05-18	| 85	| 525.0	| -1.0		| 52.50	| 51.50
BMI-450-600-578592-S	| 05-31	| 100	| 471.9	| 2.81		| 47.19	| 50.00
BMI-450-600-580608-S	| 06-14	| 115	| 471.1	| 1.39		| 47.11	| 48.50

### 4.3 Fixed-income Investment

The Synthetic POW Mining Contract decouples risks from mining difficulty fluctuation and thereby enables new financial product such as fixed income investment structure. Investors can at the same time purchase or lease physical mining rigs and start mining, and entering short positions to hedge risks regarding difficulty. If the investor’s base currency is USD, then he could also enter a short position in futures to hedge away exchange rate risk. The above method could create a fixed income product, which will allow for major capital injection into the mining space. Fixed income investors are required to manage the mining farm and mining rigs so that the mining operation runs smoothly. Their role is pivotal in connecting the synthetic mining derivatives and physical mining operations.


### 4.4 Finance Leasing

The major pain point for miners has been lacking capital to expand. Since mining risks currently cannot be hedged, no one is willing to give loan to miners. Miners now can lease mining rigs to risk-free fixed income investors or mortgage the rigs to lenders. Capital provider could require the borrowers to enter short position in both mining contract and token exchange rate, thereby stabilize their wiliness and increase their ability to repay loans.

### 4.5 Cloud Mining

A synthetic cloud mining service can be easily built upon the mining contract. The synthetic cloud mining service targets users who already understand how cloud mining work.

Traditionally, investing in cloud mining has such an economic model: user invests some amount of money to purchase cloud mining capacity and receives some mining returns daily in the period following the investment. User hopes that the total return would be greater than the initial investment. Disregarding token exchange rate fluctuation (or fully hedging exchange rate), cloud mining return only depends on mining difficulty.

Mining contract can easily simulate the above process: User purchases an array of same sized long positions of mining contract that settle in chronological order, with the lower bound of the contract index being 0. This process is very similar to cloud mining. The user will receive settlement amount from the mining contract in chronological order. The process of receiving the return mimics mining return. The amount of hashrate user purchased corresponds to the long position of the contract index. For example, the bitcoin mining contract use 10^18 hash/s as the basic unit. Therefore, purchasing one long position token is equivalent to purchasing 10^18 hash/s of cloud mining capacity. Since the lower bound of the index is 0, long position will never be liquidated, which is similar to mining.

### 4.6 Speculation

Synthetic PoW Mining Contract forms a two-sided market. In this market, unit hashrate output can be either longed or shorted. Investor could enter a long position to speculate, and become the counterparty of the hedging miner. As long as the speculator can precisely predict the difficulty fluctuation, he could be rewarded for bearing mining difficulty risks.

### 4.7  Margin Funding

For longer-term mining contracts, the Index could fluctuate in a wider range. In order for the Index not to touch the boundaries, the boundaries need to be set to a wider range. Thus, more collateral is needed in the market protocol for both long and short tokens, and drives up both tokens’ price, drives down capital efficiency. The hedging desire could also decrease since both down investment for mining rigs and hedging requires large amount of capital commitment. Therefore, we introduce variable margin (i.e dydx)
Under variable margin, a new business model arises. Lender can fund margin traders and gain risk free returns. Investor or market maker in market create long/short token pairs. They do not trade the tokens but maintain net position neutral. Margin funding lender can lend both long and short tokens to the liquidity pool of financing platform like dydx. When margin traders borrow long or short token from dydx. Margin funding lender can gain risk-free interests.

### 4.8 Market Maker

Market maker exists in all two-sided markets. Market maker makes profit by providing liquidity and bear market making risks. Since position tokens are all standard ERC-20 tokens. All market making mechanisms in the crypto world can be introduced here. Market maker can follow the traditional buy low sell high strategy by observing the orderbook. They can also profit from creating position token pairs and lend it to automatic liquidity pool like Uniswap.
