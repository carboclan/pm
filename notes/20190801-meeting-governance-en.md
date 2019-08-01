# Meeting minutes：Governance meeting，2019/8/1
The community governance meeting took place on 10 am Beijing time August 1st 2019

## Attendees：
Taylor
carboclanc
BigTreeLiuJie
Talrasha007
Mikefotiaoqing
longyunlyd
juqiangl

## Agenda Review
The [agenda](https://github.com/carboclan/pm/issues/56) has been approved

## Logic to combine the 4 trading actions on market protocol [issue 57](https://github.com/carboclan/pm/issues/56) 

Buy long= sell short
Buy short = sell long
Buy long and buy short both occur=mint new pair
Sell long and sell short both occur=redeem

The combined effect: a future like derivative that has lower and upper bound. Can be long or shorted.
Has a fixed collateral that cannot be topped up. The nominal price of the contract should be the index, which is essentially the long token price + the floor. The long token price* quantity in effect is the maintenance margin

Jie is developing the combined version of market protocol on a forked hydro protocol. 
Logic can be given but a detailed product document won't be available until later.
The combined version of market protocol can also be deployed on other  centralized exchanges easily.


## Target User
The prerequiste of designing a product must include identifiing the right target user.
For hedging it could  include mid to high level miner. For trading and speculation, the expertise required is significant. Casual trader and miner like Xinhao won't participate. Has to be Tal or Jie or ZT level trader.

Tal  as a arbitrage trader would like to see more third party data like the nicehash spot price
Jie stated three major parameters before: implied difficulty, implied average difficulty increase in each cycle,  implied profit margin

## On how to predict next difficulty. 
Two ways to calculate:
	1. Use the past 2016 blocks.
	2. Use the current cycle blocks (grow from 0 to 2016)
	Both have sound logic that should be considered.
	
The hashrate 2016 1008 and 504 can also be taken into consideration.

## Data that should be displayed alongside the orderbook:
Implied difficulty

Implied average difficulty increase

Implied leverage

## Calculator:
At least two ways to  appraoch
	1. Input average difficulty increase
	2. Input each of the diffciulty change included in the contract

Data item like premium/discount, profit margin, should be secondary if not completely gone.


## Other Projects under Yellow hat dao

Projects from our own: hashedge the cloudmining platform, coincow the game.

Projects by Professor Burak

Project with radical market

Project by Suji and Minaji

The consititution of this organization need to be formulated. Then the rules for admission and rules for projects to gain resources from the organization can be set.
