```
const tokenAmounts = PoolUtil.getTokenAmountsFromLiquidity(
    position.data.liquidity,
    PriceMath.tickIndexToSqrtPriceX64(pool.data.tickCurrentIndex),
    PriceMath.tickIndexToSqrtPriceX64(position.data.tickLowerIndex),
    PriceMath.tickIndexToSqrtPriceX64(position.data.tickUpperIndex),
    false
  );


const tokenAAmount = tokenAmounts.tokenA / (10 ** TokenADecimals);
const tokenBAmount = tokenAmounts.tokenB / (10 ** TokenBDecimals);


```