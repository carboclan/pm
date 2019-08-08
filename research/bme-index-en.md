## BTC Mining Earnings Index (BME Index)

### 1.Design Considerations
- The index MUST has a clear physical meaning.
- The index SHOULD be relative to the mining difficulty only, which makes the index easy to predict.
- The index SHOULD make the derivative on the index easy for miners(hedgers) to trade. Thus, the miners could hedge the mining risk of a period of time by entering a position of the derivative contract.
- The index SHOULD be comparable with some well-known number, such as the numbers in btc.com

### 2.Naming
The index names "BTC Mining Earnings N days Index", shorts for _BME{N}_, for example BME28, BME84 and so on.

### 3.Meaning
The BTC Mining Earnings Index (_BME_) represents **average daily bitcoins mined with 1T/s hashrate over the last N days**.

1T = 10<sup>12</sup>

### 4.Formula
_BME_ is calculated as following:

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\small&space;\mathit{BME}=\frac{1}{T}\sum_{i=1}^{T}\frac{\mathit{K_i}}{\mathit{Difficulty_i}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\small&space;\mathit{BME}=\frac{1}{T}\sum_{i=1}^{T}\frac{\mathit{K_i}}{\mathit{Difficulty_i}}" title="\small \mathit{BME}=\frac{1}{T}\sum_{i=1}^{T}\frac{\mathit{K_i}}{\mathit{Difficulty_i}}" /></a>

Where:
- **_T_** represents the number of difficulty adjustments during N days. **Let T=N/14**
- **_Difficulty<sub>i</sub>_** represents the value of difficulty after the i-th last difficulty adjustment
- **_K<sub>i</sub>_** is a scaling factor calculated as below:

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\small&space;\mathit{K_i}=\frac{\mathit{HashrateUnit}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i&space;\cdot&space;\mathit{NBlock}}{&space;2^{^{32}}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\small&space;\mathit{K_i}=\frac{\mathit{HashrateUnit}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i&space;\cdot&space;\mathit{NBlock}}{&space;2^{^{32}}}" title="\small \mathit{K_i}=\frac{\mathit{HashrateUnit} \cdot \mathit{TargetBlockTime} \cdot Coinbase_i \cdot \mathit{NBlock}}{ 2^{^{32}}}" /></a>

Parameter | Value | Note
------| -----|-------
_HashrateUnit_  | 10 <sup>12</sup> Hash/s  | 1T hash |
_TargetBlockTime_ | 600 s | Target block time for bitcoin is fixed at 10 minutes
_Coinbase<sub>i</sub>_  | 12.5 BTC per Block | The block reward at i-th last mining difficulty adjustment. <br/>Block reward halves every 21,000 blocks.
_NBlock_ | 144 | Number of blocks per day
**_K<sub>i</sub>_**| **251457095** | havles as _Coinbase<sub>i</sub>_ halves

### 5.Notes
- As the difficulty adjusts every 2016 blocks, which is roughly 14 days, the N of the index is set to be a multiple of 14. 
- The index is changed whenever the difficulty adjusts before next block reward halves.
- The index is comparable with the "mining earnings" of btc.com. Especially, BME14 should be the same with the "mining earnings" of btc.com

### 5.Examples
Height  | Time                | Difficulty        | BME14     | BME28     | BME84
--------| --------------------|-------------------|-----------|-----------|--------
572,544 | 2019-04-21 09:54:28 | 6,353,030,562,983 | 3.958E-05 |           |  
574,560 | 2019-05-04 16:32:13 | 6,702,169,884,349 | 3.752E-05 | 3.855E-05 |  
576,576 | 2019-05-18 16:31:36 | 6,704,632,680,587 | 3.750E-05 | 3.751E-05 |  
578,592 | 2019-05-31 06:43:04 | 7,459,680,720,542 | 3.371E-05 | 3.561E-05 |  
580,608 | 2019-06-14 09:03:50 | 7,409,399,249,090 | 3.394E-05 | 3.382E-05 |  
582,624 | 2019-06-27 10:59:30 | 7,934,713,219,630 | 3.169E-05 | 3.281E-05 | 3.566E-05
584,640 | 2019-07-09 17:17:48 | 9,064,159,826,491 | 2.774E-05 | 2.972E-05 | 3.368E-05

More [BME Data](BME.md)
