# SF Blockchain Week -  Defi Hackathon Recap
## TL;DR
- The Defi Hackathon capped 2019 San Francisco Blockchain Week, with a total of 56 project submissions from over 400 hackers. Check out all submissions on [Devpost](https://defi-hackathon.devpost.com/submissions).
- DeFi product innovation is getting sophisticated and fun! At least 3 projects building DeFi options/insurance, and 5 gamified DeFi constructs. 
- DeFi beyond Ethereum: 31 projects built on Cosmos.
- Our project, [Liqui3D (Game of DEXes)](https://github.com/carboclan/liqui3d), won the Best project - Grand prize & Tier 1 prize for the Tendermint Cosmos Chanllenge. 

## About Defi Hackathon 2019 @ SF Blockchain Week
San Francisco Blockchain week is a week packed of talks, project showtimes and workshops. One of the unexpected highlight of the blockchain week has been an "unconference" - [Macro.WTF](http://macro.wtf/), which explored macroeconomic perspectives on crypto. 

SFBW climaxed with a Defi hackathon that attracted more than 400 hackers from all over the world who aim to transform the traditional financial products into transparent and permissionless solutions built upon decentralized networks.

About 56 projects have been submitted at Defi Hackathon 2019. Cosmos attracted the greatest number of teams - a total of 31 projects competes for three tiers of the Cosmos challenges. The pie chart below shows the number of submissions by sponsors' challenge categories.

![Submission by Challenge Category](https://i.imgur.com/T4Biufp.png)

Besides all the sponsor prizes, there is a grand prize that honors the best team who built the best product at this hackathon (yes, that's us!). This made us the only team who won both Tendermint Cosmos Challenge Tier 1 and the Grand Prize.

## Project Highlights - Top 5
(Let me know if we missed anything) -> chuqiao: Is this part of the article or just a message to me? - article

* ### [Liqui3D: Game of Dexes](https://github.com/carboclan/liqui3d) (Grand Prize Winner + Tendermint Cosmos Challenge Tier 1 Winner)

#### Fomo3D x Liquidity Mining ([Devpost](https://devpost.com/software/liqui3d-by-team-adjust) | [Doc](https://docs.google.com/document/d/14VyCw5Ir7mJ9DbZzCXVJHuzJhVoUgr9Jbe2cWkHTe_Y/edit?usp=sharing) | [Github Repo](https://github.com/carboclan/liqui3d))
Liqui3D: Game of DEXes is a gamification of trading activity on a DEX in order to increase liquidity. Inspired by the "War of Attrition" game behind FOMO3D, we built this game to allow for the bottom-up emergence of liquidity, particularly among less popular cryptoasset pairs that fall in the long-tail of all traded cryptoasset pairs on a DEX.
![](https://i.imgur.com/FDoehxC.jpg)

### How does it work
#### Game Start
Multiple players place trades of a given trading pair (like ETH-BTC, DOGE-ETH). The transaction fees - typically a percentage of the traded amount - associated with their trades are collected in the pot.

In the beginning, the POT contains the sum of all transaction fees from all players who have placed trades of this specific trading pair. Depending on how big is your order and how liquid this trading pair is, there will be some transaction fees. The transaction fees is directly proportional to the amount being traded The transaction fees is inversely proportional to the liquidity of the trading pair.

For example, the initial transaction fee is 1%, if only 10 trades happened in the last 5 mins, we are going to increase the transaction fee, because traders would be willing to pay a little more to make the trade happen faster. If the trading pair is very popular, like ETH/BTC, the transaction fee will be very low, because there is no need to increase liquidity at this point.

The POT smart contract details the amount of transaction fees that belongs to each player. A portion of the Amount in POT continuously remains in the POT, and the remaining portion of it is given as a contribution to the global lottery pool.

![](https://i.imgur.com/Ct2yTz4.png)


#### Game Timer
The countdown will start after a certain pot size. The init countdown is 1 minute. When any trade happens, the countdown timer will accumulate a little more time. The max countdown time is 1 hour. If there is no trade happen when the countdown comes to 0, this round ends.

![](https://i.imgur.com/Vuzxg5X.png)

#### Dividend Model
The trading transaction fees collected from all players is pooled into the local_lottery_pool. 10% of the cumulative amount from the pot gets assigned as the lottery_prize.

Every 24 hours, one player out of all the existing players is randomly chosen. The chosen player wins the lottery_prize.

The likelihood of winning is proportional to the player’s relative contributions to the pot. i.e. the amount of transaction fees they contributed to the pot cumulatively.

P(Player1 wins) = (Player1's total contributions to the POT) / (Total amount in POT)

#### End of game
When round ends, the last person who made the trade will take 50% of the pot, the 25% of the pot money goes back to the participants, the last 25% goes to the next round.

If the game just goes on forever, at some point, we will distribute some of the pot money back to the participants.



* ### [Delta Protocol](https://devpost.com/software/delta-protocol)
#### Inspiration
Any products built in the decentralized finance ecosystem are susceptible to risks from the protocols they are built on top of. This includes both hack risk and systemic financial risk in the case of black swan events like runs on money markets, stablecoins losing their peg etc. These risks have the potential to collapse this entire ecosystem currently worth ~$600M.

#### What Delta Protocol do
The details of Delta Protocol is described in [this paper](https://github.com/aparnakr/OptionsProtocol/blob/master/Options_Protocol-2.pdf). In general, delta is an insurance marketplace. Insurance providers earn premiums on their collateral and insurance buyers pay upfront for the right to protect their DeFi assets. In the case of a crisis, the insurance buyer can give up their claims on Compound / Maker in exchange for the collateral that the Insurance providers have locked up in our smart contracts. The options protocol serves as insurance against DeFi hacks and risks, specifically against Dai collapsing and Compound collapsing.

Delta protocol is built on the Ethereum blockchain in the form of smart contract. We drew inspiration from Maker, Compound and Yield designs to design our insurance protocol. We built an insurance protocol that uses put options.

(**Comment**: the Delta Protocol hackathon team has since published a whitepaper on the detailed design)


* ### [MultiDAO](https://devpost.com/software/test-hb94ki)
![](https://i.imgur.com/goXOpSp.jpg)

#### Why MultiDao
Stable coins become more and more important as they have the advantages as cryptocurrencies while eliminate volatility. Currently, a stable coin collateralizes, to the best, assets on one same chain. Now with the power of IBC, we can extend collateral to different chains, which improves the stability and adoption of the generated stable coin.

#### How does it work
MultiDao is a dappchain that maintains a stable coin that is backed by multi-chain assets. Assets from different chains can be transferred to MultiDao through IBC and put into collateralized debt positions (CDPs). This is similiar to a multi-chain multi-collateral version of MakerDao. MultiDao uses Substrate as the dappchain development framework and wrote runtime logic of MultiDao. Frontend is built with Polkadot-js framework. We also built a primitive IBC over substrate with message proof along with a relayer system.

* ### Kevin
![](https://i.imgur.com/7jX1Pr2.jpg)
Kevin is a project inspired by trading on Margin for stock securities. Kevin has the ability to buy any digital securities on Margin with a p2p platform. Individuals can serve as brokers whom provide crypto to be used as margin loan. Users can purchase digital securities on margin and use their portfolio of digital assets (crypto, security tokens, cryptokitties) as the equity collateral.

* ### [Rainbolt](https://devpost.com/software/rainbolt)
Rainbolt is a privacy preserving decentralized exchange for derivatives, built on anonymous payment channels. This project is inspired by [Dan Robinson's paper](https://pdfs.semanticscholar.org/03b0/35bc6fea62caef3455ad383cd7f8164adf2f.pdf?_ga=2.150270324.311835667.1572664300-1273586131.1572664300) and [anonymous payment channels research](https://eprint.iacr.org/2016/701.pdf) done by ZCash foundation.

Users of Rainbolt can join the network as a maker. They will look for and enter bets with someone anonymously. This is accomplished by placing funds on-chain (Cosmos) in an escrow account. On the other hand, an anonymous counterparty will commit to enter in the contract which leads to trading!

(**Comment**: How can payments on a Rainbow Channel be anonymous when you need to know whether a particular counterparty made the settlement payment?)

#### Future Work
- Implement multi-asset payment channels by leveraging IBC to integrate with coins like Terra and Agoric.
- Improve upon the on-chain privacy guarantees. - Create a friendly GUI.

## Shout Out to Cool Hacks

* #### [Burning Bitcoin](https://devpost.com/software/burning-bitcoin)
**Opt out of Bitcoin's monetary supply with a 1-way peg, never see your bitcoin again.**

Using CosmosSDK, Buring Bitcoin is a module that can validate stateless SPV proofs. Submit a stateless SPV proof to a cosmos based chain that Bitcoin was sent to an unspendable address. This mints new Bitcoin on a cosmos based chain. To enable a form of tail emission while incentivizing users to migrate, a user who submits a SPV proof of burn will receive inflation for every additional user that submits a SPV proof of burn.

* #### [Hotpot](https://devpost.com/software/hotpot-azcu7l)
Hotpot is inspired by a common Chinese rotational lending game called “和会“, meaning “Rotating Credit and Savings Association (ROSCA)" (these can also be called a 'susu' or 'tanda') , which is made of a group of close friends or family members. The game is heavily reliant on the trust and relationship among members because there is no central authority recording or implementing the transactions. The smart contract manages the ROSCA including accepting payments, tracking multiple Susu's, and managing the number of players in each.

* #### [COVEN - A Credit Union for Witches](https://devpost.com/software/coven)
If DAO's like Moloch and MetaCartel DAO's can be used to pool funds and direct them to grants, why not create a Moloch like structure where deposits earn interest, and the membership can loan it out. Creating an economic benefit for members and allowing the system to grow.


* #### [Agoric in MetaMask in Agoric](https://devpost.com/software/agoric-in-metamask-in-agoric)
This is the core integration of Agoric's SecureJS blockchain platform with the MetaMask wallet to enable developers to create seamless, secure Dapps. 


* #### [BoR // Book of Reputation](https://devpost.com/software/bor)
Inspired by the notorious Warcraft 3 app "WC3 Banlist", BoR is a game agnostic whitelist / blacklist app and unbundle reputation from game publishers & merge it back with the user.



* #### [Everett: Reloaded](https://devpost.com/software/everett-reloaded)
With the use of Everett, delegators of the Cosmos Hub are able to mint bATOMs, a secondary shadow token backed by one’s delegation position. Two important features of bATOMs - Soft Peg with ATOM and validator fungibility, ensures them as an effective solution to the problems mentioned above.



* #### [ASC Protocol](https://devpost.com/software/asc-protocol)
Inspired by GSN, which enables one to pay for another's transactions, ASC Protocol team decided to generalize the concept of mutually beneficial transactions further. ASC Protocol = Active Smart Contract/Active State Change (for Cosmos) Protocol. At a high level, ASC allows you to specify conditions under which transactions can be made on your behalf, and economically incentivizes others to fund these transactions when these conditions are met. This opens up a new paradigm of possibility within blockchains.

## Conclusion
Defi Hackthon 2019 was intense. We are seeing DeFi experimentations extend beyond the Ethereum network. As the community grows, we hope to see more and more communication and collaboration within the hacker group which inspires more collective ideas/projects. 
