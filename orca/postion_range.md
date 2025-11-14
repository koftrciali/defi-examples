```js
    const positionAdress = (await getPositionAddress("POISITION_NFT"))[0];
    const position = await fetchPosition(rpc,address(positionAdress));

    //OR
    //const position = await fetchPosition(rpc,address("POISITION_ADDRESS"));

    const pool = await fetchWhirlpool(rpc, position.data.whirlpool);
    const TokenADecimals = await getTokenDecimals(rpc, pool.data.tokenMintA);
    const TokenBDecimals = await getTokenDecimals(rpc, pool.data.tokenMintB);
    const currentPrice =  PriceMath.tickIndexToPrice(pool.data.tickCurrentIndex, TokenADecimals, TokenBDecimals);
    const lowerRange =  PriceMath.tickIndexToPrice(position.data.tickLowerIndex, TokenADecimals, TokenBDecimals);
    const upperRange =  PriceMath.tickIndexToPrice(position.data.tickUpperIndex, TokenADecimals, TokenBDecimals);

    const inrage = (currentPrice > lowerRange && currentPrice < upperRange);


    //Inverse
    console.log(`${inrage ? "Inrange" : "Out of range"} (${1 / currentPrice}) (${1 / upperRange} - ${1 / lowerRange})`);
    //Normal
    console.log(`${inrage ? "Inrange" : "Out of range"} (${currentPrice}) (${lowerRange} - ${upperRange})`);

    
    ```