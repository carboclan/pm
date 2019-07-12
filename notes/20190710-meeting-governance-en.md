# Meeting minutes：Governance meeting，2019/7/10
The community governance meeting took place on 10 pm Beijing time July 10th 2019

## Attendees：
tzhan28 
carboclanc
BigTreeLiuJie
Talrasha007
Mikefotiaoqing
longyunlyd
juqiangl

## Agenda Review
The [agenda](https://github.com/carboclan/pm/issues/27) has been approved

## 1.1 index design and contract specs
### 1.1.0  The index formula
See [issue9](https://github.com/carboclan/pm/issues/9) Candidate 4

**Conclusion**: if market protocol support enough number of digits (probably need 12 digitss) then use btc as unit of account. If not, then use satoshi. In terms of contract size, if using satoshi, then the contract size need to be divided by 10^8

In order to hedge 30 days of difficulty fluctuation, one cannot simply multiply by 30. It used to work since it was non-fungible. Buy partly 1 month, partly 2 month partly 3 month doesn’t work either.

Since we are hedging a series of fluctuating unit hashrate daily mining  output, an average of the cashflows within a period should be used. Therefore, this product is too complicated so that only professional traders can understand. It likely will not be miner or retail friendly.

## Organization & budgeting

	1. Foundation with a few for-profit projects under the arch.
	2. Do not institutionalize the organization, leave only the projects.
Past expereince suggests that a core successful project could lead to a batch of new projects. 
The core projects in Consensys is called bespoke while the peripheral ones are called hub.

**Concensus**: Budget approval . Discussion on every major proposal. Prinficle for funding is to only take long term money without promising anything that cannot be accomplished. The opinion diverge here with Jie suggesting only taking grants while mike is ok with long term investments.

**Proposal**: add daily selected topic discussion on wechat group to alleviate pressure for the biweekly meeting.
