## BME Index Future

### 1.Underlying Asset

[BME Index](bme-index-en.md)


### 2.Contract Size

The value of one contract = Multiplier * The index value

Multiplier = 10<sup>6</sup> BTC

### 3.Expiration

Each BME index future will specify an expiration date. The contract expires at 02:00:00 (UTC) on the expiration date. In order to avoid the impact of block time volatility, the expiration time is usually choosen to be 7 days after the estimated time of a difficulty adjustment. The expired contract can be settled after expiration.

### 4.Settlement

BME index futures are cash settled:
  - If the settlement index is higer than the entry price, the seller pays the buyer ( _Settlement Index_ - _Entry Price_ ) * _Multiplier_ BTC per Contract
  - If the settlement index if lower than the entry price, the buyer pays the seller ( _Entry Price_ - _Settlement Index_) * _Multiplier_ BTC per Contract

### 5.Examples

#### Example 1.
One day, Alice buy 10 BME28 index future contracts from Bob at price 2.7E-5. When the contract expires, the BME28 index is 2.9E-5. So Bob pays Alice (2.9E-5 - 2.7E-5) * 10<sup>6</sup> * 10 = 20 BTC.

#### Example 2.
One day, Alice buy 10 BME28 index future contracts from Bob at price 2.7E-5. When the contract expires, the BME28 index is 2.6E-5. So Alice pays Bob (2.7E-5 - 2.6E-5) * 10<sup>6</sup> * 10 = 10 BTC.
