## 比特币算力收益指数(BME指数)

### 1.设计原则
- 指数必须具有一个明确的实际意义
- 为了方便预测，指数应当只与挖矿难度相关
- 指数应该方便矿工进行挖矿对冲。矿工应该可以通过进入基于合约的衍生品头寸对冲一段时间内的难度波动引起的风险
- 指数应该与一个被人们熟知的数据具有可比性，比如btc.com中的某一数据

### 2.命名
本合约使用的指数称为：比特币算力收益指数，缩写为_BME{N}_ ,N表示指数天数, 例如 BME28, BME84等等

### 3.含义
比特币算力收益指数 _BME_ 表示: **1T算力在过去N天内的平均日BTC收益**

1T = 10<sup>12</sup>

### 4.公式
_BME_ 用以下公式计算:

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\small&space;\mathit{BME}=\frac{1}{T}\sum_{i=1}^{T}\frac{\mathit{K_i}}{\mathit{Difficulty_i}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\small&space;\mathit{BME}=\frac{1}{T}\sum_{i=1}^{T}\frac{\mathit{K_i}}{\mathit{Difficulty_i}}" title="\small \mathit{BME}=\frac{1}{T}\sum_{i=1}^{T}\frac{\mathit{K_i}}{\mathit{Difficulty_i}}" /></a>

其中:
- **_T_** 表示N天内的挖矿难度调整次数. **令T=N/14**
- **_Difficulty<sub>i</sub>_** 表示最近倒数第i次难度调整后的难度值
- **_K<sub>i</sub>_** 是一个缩放系数，由以下公式计算:

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\small&space;\mathit{K_i}=\frac{\mathit{HashrateUnit}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i&space;\cdot&space;\mathit{NBlock}}{&space;2^{^{32}}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\small&space;\mathit{K_i}=\frac{\mathit{HashrateUnit}&space;\cdot&space;\mathit{TargetBlockTime}&space;\cdot&space;Coinbase_i&space;\cdot&space;\mathit{NBlock}}{&space;2^{^{32}}}" title="\small \mathit{K_i}=\frac{\mathit{HashrateUnit} \cdot \mathit{TargetBlockTime} \cdot Coinbase_i \cdot \mathit{NBlock}}{ 2^{^{32}}}" /></a>

参数 | 取值 | 备注
------| -----|-------
_HashrateUnit_  | 10 <sup>12</sup> Hash/s  | 1T 算力 |
_TargetBlockTime_ | 600 s | 比特币预期出块时间，10分钟
_Coinbase<sub>i</sub>_  | 12.5 BTC | 区块挖矿收益，每21,000区块收益减半
_NBlock_ | 144 | 每天的区块数
**_K<sub>i</sub>_**| **251457095** | 随 _Coinbase<sub>i</sub>_ 减半而减半

### 5.其他要点
- 因为比特币挖矿难度每2016个区块调整一次（大约相当于14天），所以指数中的天数N一般设置为14的整数倍。
- 在挖矿减半之前，指数只会在每次挖矿难度调整的时候变化。
- 指数和btc.com的“每T收益”数据在同一量级，事实上，BME14指数应该与btc.com的“每T收益”数据相等。

### 6.例子
区块高度| 时间                | 难度              | BME14     | BME28     | BME84
--------| --------------------|-------------------|-----------|-----------|--------
572,544 | 2019-04-21 09:54:28 | 6,353,030,562,983 | 3.958E-05 |           |  
574,560 | 2019-05-04 16:32:13 | 6,702,169,884,349 | 3.752E-05 | 3.855E-05 |  
576,576 | 2019-05-18 16:31:36 | 6,704,632,680,587 | 3.750E-05 | 3.751E-05 |  
578,592 | 2019-05-31 06:43:04 | 7,459,680,720,542 | 3.371E-05 | 3.561E-05 |  
580,608 | 2019-06-14 09:03:50 | 7,409,399,249,090 | 3.394E-05 | 3.382E-05 |  
582,624 | 2019-06-27 10:59:30 | 7,934,713,219,630 | 3.169E-05 | 3.281E-05 | 3.566E-05
584,640 | 2019-07-09 17:17:48 | 9,064,159,826,491 | 2.774E-05 | 2.972E-05 | 3.368E-05

更多的[BME数据](BME.md)
