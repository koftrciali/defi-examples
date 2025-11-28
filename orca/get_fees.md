getFeesQuote

```js
const { getTickArrayStartTickIndex, getTickIndexInArray, collectFeesQuote } = require('@orca-so/whirlpools-core');
const { fetchAllTickArray } = require('@orca-so/whirlpools-client');
/**
 * getFeesQuote
 *
 * @param {import('@solana/kit').SolanaRpcApi} rpc
 * @param {Object} data
 * @param {import('@orca-so/whirlpools-client').Position} data.position - position object
 * @param {import('@orca-so/whirlpools-client').Whirlpool} data.pool - pool object
 * @returns {Promise<import('@orca-so/whirlpools-core').CollectFeesQuote>}
 */
async function getFeesQuote(rpc, data) {
  const lowerTickArrayStartIndex = getTickArrayStartTickIndex(
    data.position.tickLowerIndex,
    data.pool.tickSpacing,
  );
  const upperTickArrayStartIndex = getTickArrayStartTickIndex(
    data.position.tickUpperIndex,
    data.pool.tickSpacing,
  );

  const [lowerTickArrayAddress, upperTickArrayAddress] = await Promise.all([
    getTickArrayAddress(data.position.whirlpool, lowerTickArrayStartIndex).then(v => v[0]),
    getTickArrayAddress(data.position.whirlpool, upperTickArrayStartIndex).then(v => v[0])
  ]);

  const [lowerTickArray, upperTickArray] = await fetchAllTickArray(rpc, [lowerTickArrayAddress, upperTickArrayAddress]);

  const lowerTick =
    lowerTickArray.data.ticks[
    getTickIndexInArray(
      data.position.tickLowerIndex,
      lowerTickArrayStartIndex,
      data.pool.tickSpacing,
    )
    ];
  const upperTick =
    upperTickArray.data.ticks[
    getTickIndexInArray(
      data.position.tickUpperIndex,
      upperTickArrayStartIndex,
      data.pool.tickSpacing,
    )
    ];
  const feesQuote = collectFeesQuote(
    data.pool,
    data.position,
    lowerTick,
    upperTick
  );
  return feesQuote;
}

```