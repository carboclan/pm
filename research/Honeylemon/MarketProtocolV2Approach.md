**Open request for comments. Please refer to [Issues](https://github.com/carboclan/pm/issues) for most updated discussions, and post your questions and comments as an Issue. You may follow the best practice set by reviewer @anthonyleezhang in this brilliant thread of dicussion on Issue #39 [Thoughts on MARKET vs UMA protocols](https://github.com/carboclan/pm/issues/39) .**

## Honeylemon Economic Specification - Market Protocol V2.0 Approach
The economic specifications for all HoneyLemon transactions.

Contract Creation, performed by the Honeylemon Bot.

12 hours before the beginning of a new day, the Honeylemon Bot deploys the Market protocol contract for the next trading day. The contract of the day will be used by miners and traders to execute derivative trades.

    Parameters:
    Collateral Currency = imBTC
    Lower Bound = 0.00 imBTC
    Upper Bound = Miner Payoff Index * (1 + Necessary Collateral Ratio)
    Necessary Collateral Ratio = 35%
    Necessary Collateral = Upper Bound * Multiplier
    Multiplier = 28

Necessary Collateral Ratio determined empirically by looking at historical data. Can be re-examined in the future.
Multiplier will be set to the number of days in the settlement window.
imBTC is used as an example ERC20 representation of BTC..

Limit offer, performed by Miner

Miner approves Initial Collateral (imBTC) to offer the mining payout contracts with an offer price denominated in USDT and quantity. We do not yet know whether “offer book” (no bids on our orderbook) will be onchain or offchain.
    
    Parameters:
    Offer Currency = USDT
    Initial Approval Amount = Quantity * Mining Revenue Index  *  (1 + Initial Approval Ratio) * Multiplier
    Initial Approval Ratio = 50%

USDT is used as an example ERC20 stablecoin
Initial Approval Amount the miner approves the smart contract to withdraw this amount in the future when the offer is bought by an investor.

Cancel offer, performed by Miner

Miner sends a message to cancel the remaining size on a specific offer in the orderbook

Take offer, performed by Investor

This is written as if we have the onchain orderbook.

Investor would like to buy synthetic mining contracts, so they execute a multipart transaction from a proxy contract. The transaction has the following steps:
Withdraw imBTC from Miner’s address.
Mints Long/Short Tokens with Miner’s imBTC
Sends USDT to miner(s)
Receives Long Token
Forwards Short token to miner

Withdraw Long Payout, performed by Investor
Investor withdraws Long Payout
    
    Parameters:
    Long Payout = Quantity * Multiplier * Min(Upper Bound, MRI Settlement Value - Lower Bound)
    MRI Settlement Value = average of Mining Revenue Index over the Settlement Window
    Settlement Window = 28 day period starting on the trade date

Withdraw Short Payout, performed by Miner
    Miner withdraws Short Payout

    Parameters:
    Short Payout = Quantity * Multiplier * Max(Upper Bound - MRI Settlement Value, Lower Bound)
    

Mining Revenue Index (MRI)
Theoretical (https://github.com/carboclan/pm/issues/9  Candidate 5) vs. Empirical , Coinbase Block Reward excluding Tx Fee vs . Coinbase Block Reward including Tx Fee

For MVP, suggest we choose the Block Reward including Tx Fee (FPPS-like)
 

