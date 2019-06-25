# Meeting Notes: Governance, June 20 2019

Governance meeting held @ 2PM [UTC](http://www.timebie.com/std/utc.php) in Beijing.

**Community attendance:**

- Tian Ran (Talyor)
- Tina
- Liu Jie
- Lvzi (TAL)
- Mike

## Agenda points & Actions

### 1. Agenda review

The meeting was temporarily held without an advance communication agenda.

### 2. Action point follow ups from previous meetings

None

### 3. Community vision

- _Tina:_ POW and POS supporters coexist, they might have similar goal but disimilar path to achieve the goal. POW is more executable, as the hashrate derivative could become a executable legit business. POS side agrees on the longterm goal but think hashrate derivative could be conducted more elegantly on POS and could solve the liquidity issue of POS Staking. In order to maximize both POS and POW support and their resources, the community should be inclusive and compatible to both goals, and provide infrastucture to Web3
  - _Jie:_ Not a big fan of POS. POS liquidity problem is a lack of general concensus, not a lack of derivatives.
    - _Mike:_ seconded.
  - _Tina:_ Within one community, there can be several distinct groups focusing on different directions and share resources.
  - _Jie:_ Like GNU and Linux structure, different projects can coexist.

- _Tina:_ Our Mission is to make all coins easily minable.
  - _Taylor:_ seconded.
  - _Jie:_: is this goal too grandeurs.  If this mission is set, then hashrate derivative is only one of the many directions worth exploring. An opensource BTC ASIC mining chip could be more important.
    - _Tina:_ We could raise a big flag but focus on things with in our reach first.

- _Jie:_ My initial impulse to dive in on hashrate derivative is that I saw many investor invested tons of money but bear supersized risks. On the other hand,  mining rig manufacturers and mining field operators earned most of the profits without bearing much risks. My goal is to separate mining risks using derivatives so that risk and return corresponds.
  - _Mike:_ Jie wanted arisk revelation and efficient market. Tina wanted to lower the barrier to mine so that more people can access mining.
  - _Tina:_ Both goals can coexist. A revelation of risk can naturally lower the barrier.
	
### 4.Hashrate contract v1.0

- _Tina:_ the current version should be named v0.5. We should gradually move toward the architechure Jie proposed.
  - _Jie:_ UMA is a protocol that fit our needs closely. However, two serious problems still lies between. 1.UMA lacks portfolio margin, which makes closing position and further, marketmaking impossible. 2. UMA 's contract will terminate when one side lacks margin, thereby  cutting into the other side's interest. The contract with the lack of both  transferability   and gurantee of interest, has rendered unusable in practice. We have 3 choices: 1. use UMA as is, live with the problems. 2. Rectify UMA to fix the two aforementioned problems ourselves. 3. work with UMA to fix the problems or fork UMA
    - _TAL:_ UMA has those problems indeed
  - _Tina:_ UMA team progress slowly, we might need to do it ourselves or learn from other teams.
  - _Jie:_ I have a few questions that I need to ask UMA before make any further judgement

