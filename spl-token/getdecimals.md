```js
async function getTokenDecimals(rpc, mintAddress) {

    const mint = address(mintAddress);

    const mintInfo = await rpc.getAccountInfo(mint, {
        encoding: "jsonParsed"

    }).send();
  

    return mintInfo.value.data.parsed.info.decimals;
}

```