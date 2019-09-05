# LSDai Fixed Interest Rate Token: a puttable bond issued by LSDao
Working Draft as of 2019.09.05


## Background

We are creating a system that will automatically determine a fixed interest rate that we provide to lenders based on variable Compound Rate, and the overall performance of the existing loans outstanding.
The Fixed Rate will be priced by following a wave pattern (similar to a SIN wave): the wave is essentially determined by the rate we are providing the Insurance Pool above the Compound variable rate. The higher the rate we provide beyond the Compound rate, the closer the Fixed Rate to new lenders relative to variable Compound Rate for new positions opened. The lower that rate is, the wider the spread will be. At no time the spread will be less than 1% or more than the 4% (guesstimate of people will not entering if spread is beyond). If stays within bounds, yield will heal when we have loans entering the system with higher spread. If go out of bounds, people will not go into the system because spread is too high.
Targeting an insurance premium of 1-3%.
Initialization parameter, the insurance pool starts at 2% (median to the bounds, rounded to no decimals in percentage.
Gain from of total number of cDai between the last price check and the current price check should be  

## Opening a Fixed Interest Loan

Lender place in their collateral, Insurance Pool will match the collateral with the total amount of interest to be paid out during the term. Both sides of the collateral will be denominated in the same currency, cDai. 
Three way swap: Lender’s Dai comes in and swaps into cDai, and cDai will be paired with cDai from Insurance Pool that will cover the interest payment over the entire duration of the loan as if the loan has matured, in other words, we are fully collateralizing the entire duration of the loan. The combined amount of cDai locked in MARKET PROTOCOL collateral pool will be used to mint position tokens for the Insurance Pool (Long Token, long on Compound variable rate) and the position tokens for the Lenders (Short Token, short on Compound variable rate). 
The short position token provides the collateral backing for the LSDai (fixed interest rate token) minted. 
Thus, the lenders will receive 1 LSDai token in their wallet for exactly 1 Dai they locked up. LSDai represents the position in the LSDai lending pool that the Lender has.
Full collateralization of the loans will mean that there will be no need for additional margin deposit over the duration of the loan.

## At Contract Duration

At contract duration, the price of Short Token denominated in cDai is based on the actual Compound variable interest rate the cDai is gaining relative to the fixed rate the Short Token represents. 
The price of Short Token denominated in cDai = Number of cDai represented by Short Token / (1+ Accumulated Variable Compound Interest Rate at t* (1+ Fixed Rate of the LSDai)) 
The Long Token is worth the total value of the whole (Short Token plus Long Token) minus the value of the Short Token, denominated in number of cDai. 

## At Maturity

At Maturity Date the loan will cease to gain fixed interest for the lenders. Instead the Insurance Pool retains the future Compound variable interest generated with the underlying cDai, until the lender redeems their LSDai for Dai. 
The value of the interest accrued to Insurance Pool after maturity and prior to user redemption of the LSDai denominated in number of cDai = Amount in Dai worth at Maturity / price of cDai

LSDai positions are ERC20 tokens, and can be traded on any compatible protocol. At all time, the holder of the LSDai token will receive any interest due.

## Lender Redemption 
The Lender has the right to redeem part or all of their loans any time.
If Lender redeems LSDai and receives corresponding amount of Dai, all cDai locked in position tokens returned into Insurance Pool.
At redemption, the cDai locked in the Long and Short Position Tokens are redeemed, the portion of cDai locked in Short Token is redeemed into Dai through Compound, and returned to Lenders in exchange for their LSDai tokens. Subsequently the LSDai, Long and Short tokens will be burned upon redemption.
