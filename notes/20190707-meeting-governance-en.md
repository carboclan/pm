
# Meeting minutes：Governance meeting，2019/7/07
The community governance meeting took place on 10 am July 7th 2019

## attendees：
@tzhan28 
@carboclanc
Liu Jie
Tal
Mike
ZT
Peter
Smile face


## 1.1-1.3 Index Design & Contract Specs (issue #9)

Trading Mining Index could be similar to trading options, where Implied volatility is put on the side. Here the implied difficulty could be put next to the index.

算力收益指数本质是难度分之一，其他都是常数。

The nature of the Mining Index is the inverse of the difficulty. All else is constant.

每个随机量一个标的，不要混起来。所以不应该带入挖矿手续费，block time等其他变量。

Variables (risks) should be decoupled. So the Mining Index doesnt include variables like transcation fees and block times.

有实际意义的指数在挖矿世界可能会在小数点后面五六个零很不雅观。

Mining Index with real world meanings could have many decimals which looks messy. i.e 0.00000325btc for 1 Th/s per day.

常数两个层面，一是赋予实际意义，比如1t挖一天的产出。二是也看起来舒服，是一个小数点之前有三四位的正常数字。
另一个选项是直接用科学记数法来表示，这样把小数点后面的零都放入了科学记数法里面。

the constant have two levels of implications: first, is to give the Index a real world meaning (i.e. output per unit input), second, is to make the number a nice 3-4 digits number in the integer so that traders can easily refer to it.

The other option is to use scientific notation so that all the zeros go into the later part (10^x)


## 2.1 GNU/linux以及阿帕奇的组织架构 by Mike

![阿帕奇的思维导图](https://github.com/carboclan/pm/blob/master/微信图片_20190708021115.png)

对于参与者来说：自下而上，没有空降兵，被推选成为领导是一种个人荣誉，能力至上
It's an honor to be selected as a team leader in apache foundation. Meritocracy based, bottom up

刘杰：做的doris捐给apache了。开源组织一个问题还是外部参与者太少，公司主导的项目很难社区化。如何承接是个问题。代码方面这么多年发展下来还比较方便，营销方面等就比较难

Jie: started a project called Doris that was donated to apache in the end.One problem with open source organization is lack of outside participants. Company oriented projects can hardly turn into community driven. Difficult to onboard new participants. Codewise it's relatively mature. It's harder on the business side.

tina：解决方法是领任务然后各自去做。设计token赏罚机制，组织价值捕获与项目价值捕获两个层面要协调好。
Mike; 先定原则，实践中完善

Tina: the solution is to breakdown tasks and assign them separately to the one good at specific area. Design token economics to reward and slash participants. Value capture in organization level and project level need to be aligned
Mike: set ground rules, streamline them in practice

### 3 principles of Apache
	1. 精英主义（需要确认是不是meritocracy）对参与者要求严格，强自驱力
	2. 自下而上的晋升机制
	3. 能力和贡献值至关重要
  
  1. meritocracy
  2. bottom up & promotion oppurtunity
  3. contribution/capability based

参与方式，晋升通道：b的参与和c的参与，要看到底我们需要什么资源，谁来提供资源和价值，他们之间什么关系。针对他们设计机制。

Ways to participate: participation from both Businesses and individuals. It depends on what kind of resources does this organization need, who can contribute. How participants are related. Design mechanisms for them.

mike：linux和apache里面大部分都是商业组织完成，个人开发者比例一般。另外精英抱团比较严重。新人晋升仍然不容易，需要跟老人搞好关系

Mike: most of the works in Linux and apache are done by companys. Percentage of individual developers is not high. Old members of the community tend to work together and block promotion passage for new members.

tina：精英主义和面向大b不可取。可取的是奖励阶梯，畅通的晋升方式。无法评论的：商业组织赞助为主是时代产物

Tina: aganist elitism, don't want the organization to be mainly facing businesses. Clear path to promotion should be adopted. Cannot comment on companies donation causing current open source organization to be more business facing.

mike：管理方式：人都很强，认领了就自己搞定，会自驱
tina：三原则有点像pow+pos的结合。盈利组织可以参考steam/valve，consensys

Mike: how to manage: self-driven, 
Tina: the 3 principles are like a combo of pow and pos. Refer to Valve and consensys

## 2.2 Proposal of "Yellow Hat DAO" - to build an efficient capital market for blockchain infrastructure

相信自由市场奥派做空的人，是非主流观点。需要群策群力。
Unpopular opinions: belief in market freedom. People of similar believe need to gather together
Tina跟几个老外吃饭以后一起提出，成员包括near protocol的创始人乌克兰小哥illia ，曾提出用smart contract做跨连delegate pos，会break所有bft concensus。还有James prestwich设计过hashrate derivative，storj的联创。pow都nichehashable
总之基础设施不安全，需要为基础设施建立有效的市场。
Yellow hat 之于carboclan有点像共产国际&中国共产党。我们是在中国主力干活的组织，外援们也需要有归属，方便大家一起做事

Tina had lunch with Illia and James Prestwich who shared similar belief. Illia is the foudner of near protocol. He proposed cross chain pos delegation using smart contract. James prestwich designed hashrate derivatives a year and half ago. He is the cofounder of Storj.
On the otherhand, lots of pow chains are nicehashable. To sum up, blockchain infrastucture are not safe, an efficient market need to be built.

Yellow hat vs carbonclan : international & loosely organized vs a relatively close core group

Jie：名字有点怪，白帽黑帽只是tag不是名字，不会这么自称。

Jie: the name yellow hat is weird, White hat are tags not names. They don't call themself that.

## 2.3 collaboration on documents
三个级别的改动
第一层：简单修改直接改
第二层：表述调整就pull request 然后三个人review
第三层：大修改要开会讨论

目前三个人权限，tina 刘杰和天然

Three levels are modifications
1. simple grammar of typo, just change it
2. different wording. Use pull request and review by 3 people
3. major changes need to be discussed in meetings

3 people have write access: Tina Jie and Tianran

提issue要让所有人都看得懂，符合开源社区通用惯例
开源社区标准高于公司

Issues need to be written clearly. Follow the common practice of mature open source projects. Their standard is higher than that of companies

提pull request以后可以再提问评论，
取决于问题级别，来决定要多少人来对这事情决策，小事情一两个人就够了，大事情要让更多人参与

Pull request can be commented. Loop in necesary people to make decision on different subjects. Major issue require more participation

## Progress

Finish with 2. Only done with 1.1.1 and 1.1.3. Propose new ideas and comment on 1.1.1 &1.1.3. The rest are up for discussions next time
Keep the meeting under 2 hours next time

