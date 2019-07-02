
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

ETH Mining Index ( _EMI_ ) represents _N_ blocks prior to block height _H_, expected return in ETH given _Hashrate_ (Unit: Hash/s) in ethereum mining. _Difficulty<sub>i</sub>_ represents mining difficulty at block height _i_, _Coinbase<sub>i</sub>_ represents mining reward at block height _i_, and _TargetBlockTime_ represents expected block time of the ethereum network. _EMI_ is calculated as following:

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\small&space;\mathit{EMI}=\sum_{i=H-N}^{N-1}\frac{\mathit{Hashrate}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i}{\mathit{Difficulty_i}\cdot&space;2^{^{32}}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\small&space;\mathit{EMI}=\sum_{i=H-N}^{N-1}\frac{\mathit{Hashrate}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i}{\mathit{Difficulty_i}\cdot&space;2^{^{32}}}" title="\small \mathit{EHRI}=\sum_{i=H-N}^{N-1}\frac{\mathit{Hashrate} \cdot \mathit{TargetBlockTime} \cdot Coinbase_i}{\mathit{Difficulty_i}\cdot 2^{^{32}}}" /></a>

Given block height _H_, _Difficulty<sub>i</sub>_ and _Coinbase<sub>i</sub>_ are the only variables in the formula dependent on block height, all other terms are constants. In other words, _EMI_ only depends on mining difficulty and per block reward. _EMI_ parameters are defined as following:

Parameter | Value | Note
------| -----|-------
_Hashrate_  | 1,000,000,000,000 Hash/s  | |
_N_  | 80640  | 14-day window
_Coinbase<sub>i</sub>_  | 2 ETH | Block reward is 2ETH starting from block height 7,080,000
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

At settlement, Market Protocol smart contract will send ETH to addresses that hold contract position tokens. Long token holder will receive ( _EMI_ - _Floor_ ) in ETH per Contract, short token holder will receive ( _Cap_ - _EMI_ ) in ETH per Contract.

#### Margin

Issuer of the Tokenized Synthetic Ethereum Mining Contract needs to send ( _Cap_ - _Floor_ ) amount in ETH to the Market Protocol smart contract as collateral in order to mint contract position tokens. Contract positions are fully collateralized with no need to top up margins prior to settlement.

#### Naming Convention for Contract Position Tokens

EMI-\<Floor\>-\<Cap\>-\<Height\>-[L|S]

- Floor: Index lower bound
- Cap: Index upper bound
- Height: block height for settlement
- L: long position
- S: short position

Example: EMI-100-200-80000-L token corresponds to a long position on a ethereum minning contract with Index valid range of [100,200], to be settled at block height 80,000.


###  2.2 Synthetic BTC Mining Contract
#### Index








