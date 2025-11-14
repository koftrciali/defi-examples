Get price from orca

```js

const {PriceMath} = require('@orca-so/whirlpools-sdk');
const { fetchWhirlpool } = require('@orca-so/whirlpools-client');
const poolAdress = address("Czfq3xZZDmsdGdUyrNLtRhGc47cXcZtLG4crryfu44zE"); // SOL/USDC orca pool

const TokenADecimals = 9; // WSOL decimal
const TokenBDecimals = 6; // USDC decimal
const pool = await fetchWhirlpool(rpc, poolAdress);


console.log(PriceMath.tickIndexToPrice(pool.data.tickCurrentIndex,TokenADecimals,TokenBDecimals));
// 141.097789487691039880198609536386712585 :(


```