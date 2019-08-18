**Open request for comments. Please refer to [Issues](https://github.com/carboclan/pm/issues) for most updated discussions, and post your questions and comments as an Issue. You may follow the best practice set by reviewer @anthonyleezhang in this brilliant thread of dicussion on Issue #39 [Thoughts on MARKET vs UMA protocols](https://github.com/carboclan/pm/issues/39) .**

# Hashedge: A Decentralized Marketplace for Crypto Mining & Staking Output

## 1. Motivation

Generalized mining is a big yet primitive market. In 2018, a total of over US$ 9 billion worth of POW mining rewards (BTC 698,448 worth US$ 5.4 billion & ETH 7,431,815 worth 3.6 billion) were awarded to miners as block rewards and transaction fees. In 2019, with the gradual launch of POS networks, existing market for generalized mining is estimated to be over US$ 10 billion (an estimated US$ 2.5 billion worth of cryptos are POS network rewards according to Staked.us). 

Miners have accounted for significant demands for liquidity for years due to the capital-intensive nature of the business. Hedging demand emerges recently as more institutional investors enter the market after the latest crypto winter. Current financial services for these keepers of the blockchain network (mainly miners and validators) depend heavily on trust and personal connection. 

PoW miners have traditionally resorted to selling cloud mining contracts to hedge risk by locking in future mining rewards ahead of time or earning premium for performing mining services. However, there have been few credible choices available for miners and validators of small to medium size operations to list their mining services.

On the other hand, investors who are interested in mining and staking cashflow without having to deal with the hassle of actual mining, only have the choice of centralized cloud mining or staking platforms that leave them with little pricing power or choice of cryptocurrencies. Moreover, prevalent cloud mining contract design which requires investors to put up full collateral upfront but no collateral for the issuers, exposing investors to significant counterparty risk.

Despite the scam-prone nature of the market, cloud mining contract market leader Genesis Mining retained over 2 million registered users. Hashrate spot marketplace Nicehash has over 100K DAU even in a bear market. Existing cloud mining market is far from standardized or efficient. Price disparities of 30-80% for the same type of mining contract underwritten by different platforms is common.

Therefore, we are building Hashedge, a peer-to-peer marketplace where contracts of future mining and staking outputs can be freely traded. We would like to offer investors services provided by collateralized keepers of the network, in a permissionless market with pricing transparency and trust-minimized infrastructures.

## 2. Hashedge Overview

HashEdge is a peer-to-peer marketplace where contracts of future mining/staking cash flows can be traded. It is a one-stop-shop for anyone who would like to earn protocol-governed passive income through participating in a blockchain network, without the hassle of setting up mining or staking operations, or the worry about platform scam or counterparty risks. 

Any blockchain network service provider (e.g. a miner or a validator) can “sell” their output to earn service fee, obtain capital to scale up operation or lock in potential profit in advance to hedge their risk, all by simply listing a mining contract. 

Anyone who buys the contract can expect mining/staking payout directly from a miner or validator. The contractual agreement between the buyer and seller are enforced via smart contracts. All transactions will be settled on chain with immutable records. Counterparty risks are strictly managed with on-chain collateralization.

A credit system built around decentralized identities systematically rewards “good actors”: longer transaction history and better track record of a seller would translate directly into higher rankings of his/her listing and less margin/collateral requirements. This helps create a virtuous positive-feedback loop.

## 3. Synthetic Mining & Staking Cashflow Contract

### 3.1 Generalized Mining Index

HashEdge Generalized Mining Indices are a series of generalized reference Indices that capture the average mining yields over certain periods of time for various minable cryptos. These indices also serve as referencing indices for the settlements of generalized standard synthetic mining contracts on HashEdge.

The following is an illustration of  the algorithm to calculate the ETH Index.

#### 3.1.1 Configurable Parameters

Int N: Size of the rolling window (in terms of number of blocks)

#### 3.1.2 Data

Di:  Difficulty of the ith most recently generated block, with D0 being the latest block
BRi: Block reward of the ith most recent block

#### 3.1.3 Calculation

Index = C * sum(Di * BRi * wi) / sum(wi) , i from 0 to N-1,
wi = (N – i)/N,
and C is the normalizing factor set to 20 (since 1GH/s of total network hashrate approximately translates into 20 TH of difficulty).

#### 3.1.4 Meaning and Observations

- The index approximately depicts how many ETH 1GH/s of mining power can produce per block. 
- The index is smoothed over a period of N blocks.
- The index is a simple time-weighted average assigning more weight on more recent blocks.
- The index refreshes itself every block rather than per fixed time length.
- All data can be found on-chain (thru etherscan.io for example) and thus the data are 100% transparent without any possible adulteration.
- The value of N needs to be determined according to (perhaps) the convention of miners or pools. However, since the index is used for derivative contract settlement, it cannot be changed for the same contract once set.

### 3.2 Cashflow Swap

A swap is a typical derivative contract through which the counterparties exchange (swap) cashflows or financial instruments. A common example of a swap contract is the interest rate swap.

A HashEdge mining/staking contract entitles the payer (buyer) the floating leg of future cash flows from the receiver (the issuer) and the receiver the fixed leg, in accordance with a predetermined set of schedules and rules. 

The fixed leg and the floating leg may not be (and are usually not, in our case) denominated in the same currency.

These contracts are hashrate swaps in nature. (See Contract Specs and Margin)

On the other hand, to mitigate counterparty risk (credit risk), HashEdge may adopt a pseudo margin system to ensure the actual exchange of cashflows. With such mechanism, some cashflows may happen upfront as margin deposits. 

### 3.3 Contract Specs

- Fixed leg denominator: DAI
- Floating leg denominator: DAI, ERC tokens
- Contract size unit: hashrate unit of the underlying floating leg token
- Quote unit: DAI (tokenized swap contracts are purchased with or sold for DAI) 
- Tenure structure: 3-month long contracts rolling every month, expiring on the 28th of each month. 
- Payment (cashflow) schedule: every 1 day starting from 24 hr after the kickoff of each contract. The last cashflow happens on the expiration date. 
- Reference Index: Average Total Hashrate*. Reference Index are used to determine the size of the payment of the floating leg.
- Actual payment of the floating leg at each exchange of cashflow: Contract Size/Average Total Hashrate

## 4. Margins & Trading

### 4.1 Margin Overview

HashEdge adopts a pseudo-margin system to ensure the cashflows of contracts happen in accordance with its original schedule. This pseudo-margin system could be implemented either as part of a centralized exchange, or with smart contracts by leveraging the features of ERC721 tokens. 

In the rest of this literature, we describe the latter approach. HashEdge swap contracts are embedded in ERC721 tokens and the margin system are implemented with smart contracts.

Swaps are often traded OTC. HashEdge provides an auction marketplace for the ERC721 tokens embedding the hashrate swap.
A HashEdge swap token entitles its owner to receive the floating leg of the contract, also entitles the issuer the fixed leg.

### 4.2 Issuance

An initial margin of x% of the expectation of all future cashflows (on both sides) are locked in the smart contract to mitigate credit risk. 

When the token is issued, the initial (first) buyer pays to own the token which generates future floating cashflows. The schedule of such cashflows are described in Contract Specs. 

The payment of the initial buyer does NOT go to the seller directly but instead locked in the smart contract as initial margin and will be released to the seller at each cashflow. The issuer (the seller) also locks the expected value of total future floating leg payments into the smart contract. 

For the initial offering, a Dutch Auction mechanism similar to the one for US treasuries are used.

### 4.3 Cashflows & Margining

A standard swap contract (contract) is a swap contract according to which cashflows are exchanged based on some synthetical reference rate.

The contract holder who pays the fixed leg is referred to as the buyer, the buyer’s counterparty who pays the floating leg the seller.

#### 4.3.1 The Margin System

To enter into a position of such contract, a margin system is required. The margin system consists of the following components.

##### 4.3.1.1 A place (may be a smart contract etc.) to hold the buyer’s margin.

##### 4.3.1.2 A place to hold the seller’s margin.

##### 4.3.1.3 Margin calculation (e.g. Initial Margin and Maintenance Margin) logic.

For simplicity we assume the platform allow for a max leverage ratio of L for one leg, then for that leg the initial margin.
=  Max(expected next payoff * (1+buffer),  /L * total expected payoff of the next n payments)
,where buffer, L, and n are configurable parameters (perhaps only by the platform)

The maintenance margin  
= Max(expected next payoff * (1+buffer2), p * 1/L * total expected payoff of the next n payments)
,where buffer2, p are parameters.

For illustration purpose, we hereafter use the following value for these parameters. 
- buffer = 0.5
- buffer2 = 0.5
- l = 5
- n = 10
- p = 0.5

##### 4.3.1.4 Liquidation logic.

If for some reason the remaining margin of any leg of a contract falls below the maintenance margin, the contract position shall be liquidated in favor of the payer of the other leg. 

During the process of a liquidation, part or all of the remaining balance of each leg shall be returned to the payer or paid to the receiver (rule and parameters to be further discussed).

Liquidation is performed every x seconds and are timed individually for each contract. 
x = 7200 in our example.

##### 4.3.1.5 Swap payoff (cashflow exchange) logic.

At each payoff time, a smart contract automatically distributes payoffs to their corresponding receivers according to predetermined schedule and the reference rate at that time.

#### 4.3.2 The margin system also supports secondary market trading.

Now we illustrate how a holder of the contract can transfer his/her position to another. 

Note 1. that this document only describe how margin works during a position transfer. How orders are matched are not within the scope of the document (order book might be one solution however).
Note 2. Currently we only support the buyer of the contract to transfer (sell) his/her position. The issuer of the contract currently is not able to transfer his obligation.

- During the process of a position transfer, the margin of the floating leg does not change at all.
- The price of the transfer is determined by the market. 
- Any extra fixed leg margin locked in the contract above the maintenance margin will be returned to the current owner of the contract before the transfer, in addition to the price paid.

This means that after each successful transfer, the contract would only have a fixed leg margin value equal to the maintenance margin.

- Once a contract’s ownership transfers, the liquidation timer resets, giving the new owner x seconds to deposit extra margin.

### 4.4 Secondary Market

The token can be traded in a secondary market, provided by Hashedge. Buying the token transfers the ownership to the buyer (the new owner) who now enjoys the right to receive all unpaid cash flows from the issuer according to the original schedule of the swap. Any cashflow happens before the transfer of ownership does not affect the new owner. In this case, we see the value of such tokens decreases as cash flows happen. The theoretical value of these tokens may not be monotonically decreasing due to other factors such as interest rates and hashrate volatility etc.

For the secondary market, Hashedge may provide a simple auction marketplace like Ebay or a full-fledged exchange with order books + matching algorithm.
