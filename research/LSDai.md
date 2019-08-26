**Open request for comments. Please refer to [Issues](https://github.com/carboclan/pm/issues) for most updated discussions, and post your questions and comments as an Issue. You may follow the best practice set by reviewer @anthonyleezhang in this brilliant thread of dicussion on Issue #39 [Thoughts on MARKET vs UMA protocols](https://github.com/carboclan/pm/issues/39) .**

![Technical overview of how the LSDai system works](https://challengepost-s3-challengepost.netdna-ssl.com/photos/production/software_photos/000/829/681/datas/gallery.jpg)

## Inspiration
In a world of roller-coaster crypto volatility, we turned to Dai for stability. With the emergence of interest generating instruments born through layers of collateralization on crypto native synthetic assets, we are entering a phase of interest rate volatility. Introducing LSDai, for your escape to a peace of mind: earn Compound interest on your collateral with rDai, while providing liquidity for hedges against variable Compound interest.  

Empirical studies from traditional finance have shown the adverse impact of variability in interest rates (the “price” of money) on the real economy. Accordingly, interest rate swap, used by non-financial firms in the management of the interest rate risk of their debt, is one of the most important fixed-income instrument in the trading and hedging of interest rate risk.

We have seen recent wild swings of Compound interest on Dai, going from 5% to peaking over 16% within a month. With the emergence of DeFi stack, more synthetic crypto assets composed of native assets are created and then rebundled on the Ethereum tech stack, enabling new possibilities while introducing complex interdependencies into the system. 

This is why we decided to build a tokenized interest rate swap on Dai interest, to fill in the void with an essential decentralized stabilizer for the DeFi market. 

## What it does
LSDai creates a Euro-dollar like construct, that is a future on the Compound Dai lending rate over the duration of the contract. By leveraging Market Protocol, LSDai takes on the approach of de-coupling the risk of the two sides  
It enables three different types of users to gain the kind of exposure to the interest rate fluctuation that fits their profile, while aligns incentives.

* **Hedgers**: Hedgers are lending out their Dai on Compound and earn interest, but fear that the interest rate — thus, their passive revenue — will drop. LSDai’s Market Makers mint and sell them *short Dai interest tokens* for Dai, in the amount that will completely hedge their interest-earning position. This means they will experience no fluctuation: if the interest rate drops, the profit from the short will make them even, and if the rate goes up, the extra interest makes up for their loss. Hedgers can insure themselves against loss of income.

* **Speculators**: These players have no stake in the lending business, they just want to speculate on the changes in the interest rate. Bettors expect Dai’s lending interest rate on Compound to go up or down, and buy *long* or *short Dai interest tokens* from the LSDai Market Makers for Dai. They either gain or lose money, depending on where the interest rate goes… and how clear their mind was when they made their bet.

* **Market makers**: Market makers manage the minting and selling of the *long* or *short Dai interest tokens*

## How we built it
We took a decentralized approach, adopting Market Protocol in decoupling the interest rate swap positions into margin-embedded Long and Short position tokens. We used Airswap to find the price of the Long ad Short position tokens. Given the importance of liquidity in the model, we programmed a bot to arbitrage away the spread across the Market Makers (Minters) of the token pairs and the Hedgers/Speculators.

Lastly, in order to create virtuous loop to further incentivize the Market Makers, we implemented rDai as the collateral in Market Protocol in Minting of the position pair. Thus, Market Makers will be able to earn interest from the rDai collateral, in addition to earning the spread.

For this hackathon, we are able to start from scratch and launch our LSDai on Ethereum Main Net. Since we are the first Market Maker in this product, we have decided to donate the interest accrued from rDai in the collateral to EthBerlin. 

## Challenges we ran into
Figure out how to take a contract that is written to provide assets priced in dollars and invent a pricing structure for the interest rate swap, and how the pricing structure may fit into the existing Market Protocol smart contract that we have already deployed on Kovan. 

We encountered a hard coded Infura key that hit its rate limit today in the Airswap widget, and the widget code is not open sourced. We downloaded each file until we got to the one that had the hard coded Infura key, replaced the key with our own and uploaded the entire file structure to private services to re-serve it to our app. 


## Accomplishments that we're proud of
1. Build from scratch and launch on Main Net!
2. Created an innovative solution of decentralized interest rate swaps for DeFi.
3. Aligned a global team from 3 continents. Met at EthBerlin, and start from scratch, ideation to launching on Ethereum Main Net in less than 30 hours.  

## What we learned

## What's next for LSDai
We plan to fix up the front end bug and roll out a new version based on the updates on rDai 2.0 contract, in September. A truly **Stable-revenue-stable-value synthetic token** is coming. Stay tuned!
