
# Meeting minutes：Governance meeting，2019/7/07
The community governance meeting took place on 10 am July 7th 2019

## attendees：
tzhan28 
carboclanc
BigTreeLiuJie
Talrasha007
Mikefotiaoqing
longyunlyd
juqiangl

## 1.1-1.3 Index Design & Contract Specs (issue #9)

Note: Issue 9 is essentially about the trade off of Index scale, and Contract Size (which affects position tokens).
The key considerations: ease of understanding of Index, v.s. ease of referring to Index, v.s. ease of understanding of how many contract tokens to buy given a certain need for hedging. 

Trading Mining Index could be similar to trading options, where Implied volatility is displayed on the side. Here the implied difficulty could be displayed next to the Index.

算力收益指数本质是难度分之一，其他都是常数。

The nature of the Mining Index is the inverse of the difficulty. All else is constant.

每个随机量一个标的，不要混起来。所以不应该带入挖矿手续费，block time等其他变量。

Variables (risks) should be decoupled. So the Mining Index doesnt include variables like transcation fees and block times.

有实际意义的指数在挖矿世界可能会在小数点后面五六个零很不雅观。

Mining Index with real world meanings could have many decimals which looks messy. i.e 0.00000325btc for 1 Th/s per day.

常数两个层面，一是赋予实际意义，比如1t挖一天的产出。二是也看起来舒服，是一个小数点之前有三四位的正常数字。
另一个选项是直接用科学记数法来表示，这样把小数点后面的零都放入了科学记数法里面。

The constant here has two levels of implications: 
1. Give the Index a real world meaning (i.e. output per unit input).
2. Make the number a 3-4 digits number in the integer part so that traders can easily refer to it.

The other option is to use scientific notation so that all the zeros go into the later part (10^x)


## 2.1 GNU/linux and Apache Software Foundation

![阿帕奇的思维导图](https://github.com/carboclan/pm/blob/master/notes/images/apache-arch.png)

对于参与者来说：自下而上，没有空降兵，被推选成为领导是一种个人荣誉，能力至上
Among contributors it is meritocracy based, voted up by members, and it is an honor to be selected as a leader in Apache.

刘杰：做的doris捐给apache了。开源组织一个问题还是外部参与者太少，公司主导的项目很难社区化。如何承接是个问题。代码方面这么多年发展下来还比较方便，营销方面等就比较难

Jie: worked on a project called Doris in Baidu, that was donated to Apache in the end. One problem with open source organization is lack of freelance participants outside of major organizations. Company oriented projects can hardly turn into community driven. Difficult to onboard new participants. Apache's organizational structure is good for code contribution. It's harder to quantify contribution from the business side.

tina：解决方法是领任务然后各自去做。设计token赏罚机制，组织价值捕获与项目价值捕获两个层面要协调好。
Mike: 我们需要先定原则，实践中完善

Tina: To quantify and reward non-coding contribution, will entail clear definition of tasks and mechanism that encourages partcipation. It will likely involve token reward and punishment mechanism. Design token economics to reward and slash participants. Value capture in organization level and project level need to be aligned
Mike: let's set ground rules first, then figure out the mechanisms based on these ground rules

### 2.3 principles of Apache
	1. 精英主义（需要确认是不是meritocracy）对参与者要求严格，强自驱力
	2. 自下而上的晋升机制
	3. 能力和贡献值至关重要
  
  1. meritocracy-based, high requirement of participation, self-driven;
  2. bottom up internal promotion mechanism;
  3. quantified contribution & capability

参与方式，晋升通道：b的参与和c的参与，要看到底我们需要什么资源，谁来提供资源和价值，他们之间什么关系。针对他们设计机制。

Ways to participate: participation from both Businesses and individuals. It depends on what kind of resources does this organization need, who can contribute. How participants are related. Design mechanisms for them.

Mike：linux和apache里面大部分都是商业组织完成，个人开发者比例一般。另外精英抱团比较严重。新人晋升仍然不容易，需要跟老人搞好关系

Mike: most of the works in Linux and apache are done by companys. Percentage of individual developers is not high. Old members of the community tend to work together and block promotion passage for new members.

Tina：精英主义和面向大b不可取。可取的是奖励阶梯，畅通的晋升方式。无法评论的：商业组织赞助为主是时代产物

Tina: aganist elitism, pro meritocracy. Don't want the organization to be mainly facing businesses. Clear path to promotion should be adopted. Apache turned out to heavily rely on corporate donation or sponsorship may be a product of the past. We can do things differently now.

mike：管理方式：人都很强，认领了就自己搞定，会自驱
tina：三原则有点像pow+pos的结合。盈利组织可以参考steam/valve，consensys

Mike: Something to learn from Apache, how to manage: self-driven.
Tina: the 3 principles are like a combo of pow and pos. Refer to Valve and Consensys.

## 2.2 Proposal of "Yellow Hat DAO" - to build an efficient capital market for blockchain infrastructure

创建区块链基础设施的衍生品金融市场，因为会影响协议为保障其安全所设计的经济机制，就如同做空这个概念会是非主流的，可能会得罪项目方。但我们实则通过创建有效的金融市场，通过杠杆，做空，让好的协议更好的胜出，让共识小的协议的安全性问题暴露。有争议的世界最大的算力交易市场Nicehash是有价值的，在为矿工和算力需求方提供一个高效的交易市场的同时，也让人可通过付出成本购买算力的形式指定算力来攻击其他公链获利（为此社区计算出了各公链基础设施的“Nichehash-able”攻击成本），但是也让社区更清晰认知各链协议的安全性问题。需要凝聚一群奥派经济学相信自由市场力量的伙伴群策群力。
Creating derivatives on PoW and PoS effectively is creating external incentives that can threaten the economics of some weaker protocols. Many protocol foundations may not like us. Just like shorting, it is not popular amongst mainstream. However, what we are doing is accelerating the market process, and create pressure on protocols to create defense against these attacks. The largest Hashrate spot market Nicehash has always been controversial. While having created an efficient trading marketplace for miners and their counterparties, it enable people to buy hashrate and conduct attacks on other chains at a cost (so-called Nicehash-able cost), but also raised awareness regarding the security issues that the protocols are facing. We should band together with other folks who believe in Austrian School of Economics and the free market.

黄帽联盟这个组织是在Tina跟几位公链协议创始人和意见领袖独立日聚会提出的。其中Near Protocol的创始人，曾提出用智能合约创建通过类衍生品机制实现跨链代理质押，这个机制会有可能break所有bft concensus。另外，参与者当中，Summa的创始人，原Storj联合创始人James Prestwich设计过算力保险。

“Yellow Hat DAO” idea is created during a meetup with a few protocol founders/architects. Amongst the participants, Illia, co-founder of Near Protocol, has written a piece on "Staking & Delegation via Smart Contract", using smart contract and derivative like approach to achieve cross-chain delegation network, which can threaten essentially the weaker BFT consensus. Other participant include founder of Summa One and co-founder of Storj James Prestwich, who has designed Hashrate Insurance in the past. 

黄帽联盟相对于碳基部落CarboClan，部落是发起方，黄帽联盟是国际组织？
Yellow hat vs carbonclan : international & loosely organized vs initiator？

Jie：名字有点怪，白帽黑帽只是tag不是名字，不会这么自称。

Jie: the name yellow hat is weird, Black Hat and White Hat are tags not names. They don't call themself that. May need to verify the name with other hackers.

## 2.3 collaboration on documents

三个级别的改动
第一层：简单修改直接改
第二层：表述调整就pull request 然后三个人review
第三层：大修改要开会讨论

目前三个人权限，tina 刘杰和天然

Three levels are modifications
1. simple grammar of typo, just change it
2. different wording. Use pull request and review by 3 people
3. major changes need to be discussed in governance calls

3 people have write access: Tina, Jie and Tianran

提issue要让所有人都看得懂，符合开源社区通用惯例
开源社区标准高于公司

Issues need to be written clearly. Follow the common practice of mature open source projects. Their standard is higher than that of companies

提pull request以后可以再提问评论，
取决于问题级别，来决定要多少人来对这事情决策，小事情一两个人就够了，大事情要让更多人参与

Pull request can be commented. Loop in necesary people to make decision on different subjects. Major issue require more participation

## Progress

Finish with 2. Only done with 1.1.1 and 1.1.3. Propose new ideas and comment on 1.1.1 &1.1.3. The rest are up for discussions next time
Keep the meeting under 2 hours next time

