---
description: Some common issues and things to look out for when building your plugin
---

# Common Pitfalls

### ETH conversions

In a lot of swap based projects, ETH (or other native tokens) is first converted to WETH before being included in the swap transaction. This means you may find the address for WETH in the inputs for `tokenIn` when you are expecting Ether.&#x20;

There will also be occasions where the specific project represents ETH or another native asset with a specific address string, such as `0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE`.

On our internal systems, Ether and other native assets are represented with the [zero address](https://etherscan.io/address/0x0000000000000000000000000000000000000000). Whenever the token is input as Ether or another native asset, you will need to convert it to match the expected parameter in the input.&#x20;

```typescript
let tokenOrWeth

if (tokenIn && tokenIn === zeroAddress) {
    tokenOrWeth = '0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2' // WETH
} else {
    tokenOrWeth = tokenIn
}
```

***

### Amounts Lower Than Expected

This mainly affects swaps where slippage values may affect the amounts that are present in the transaction details. These inputs are sometimes labeled as `minAmountOut` or similar. When testing keep in mind these values may be lower than expected.&#x20;

***

### Overlapping ABI Inputs

Overlapping or Overloaded ABI Inputs can lead to premature branching, where conditions unintentionally align with the wrong function's inputs. To counter this, split the ABI into distinct fragments. This ensures input comparisons are accurate and specific to each function's signature, preventing mismatches and ensuring correct logic flow in your plugin.

❌ **Combined ABI fragments with overlapping Inputs.** ❌

<pre class="language-typescript"><code class="lang-typescript">return compressJson({
  chainId,
  to,
  value: nativeIn ? amountIn : tokenIn ? 0 : undefined,
  input: {
    $abi: TRADER_JOE_ABI, // all abi fragments combined 👎
    $or: [
      {
        // exactNativeforTokens
<strong>        amountOutMin: amountOut,
</strong>      },
      {
        // exactNativeforTokens
        amountIn,
<strong>        amountOutMin: amountOut,
</strong>      },
<strong>      { amountOut: amountOut }, // nativeForExactTokens
</strong>      {
        amountInMax: amountIn,
<strong>        amountOut: amountOut,
</strong>      }, // tokensForExactTokens
      {
        amountIn: amountIn,
        amountOutMinNATIVE: amountOut,
      }, // exactTokensForNative
      {
        amountInMax: amountIn,
        amountNATIVEOut: amountOut,
      }, // tokensForExactNative
    ],
  },
})
</code></pre>

**✅ Split ABI with specific fragment being used for each condition. ✅**&#x20;

{% code title="Traderjoe.ts" %}
```typescript
return compressJson({
  chainId,
  to,
  value: nativeIn ? amountIn : tokenIn ? 0 : undefined,
  input: {
    $or: [
      {
        // exactNativeforTokens
        $abi: EXACT_NATIVE_FOR_TOKENS_ABI,
        amountOutMin: amountOut,
      },
      {
        // exactNativeforTokens
        $abi: EXACT_TOKENS_FOR_TOKENS_ABI,
        amountIn,
        amountOutMin: amountOut,
      },
      { $abi: NATIVE_FOR_EXACT_TOKENS_ABI, amountOut: amountOut }, // nativeForExactTokens
      {
        $abi: TOKENS_FOR_EXACT_TOKENS_ABI,
        amountInMax: amountIn,
        amountOut: amountOut,
      }, // tokensForExactTokens
      {
        $abi: EXACT_TOKENS_FOR_NATIVE_ABI,
        amountIn: amountIn,
        amountOutMinNATIVE: amountOut,
      }, // exactTokensForNative
      {
        $abi: TOKENS_FOR_EXACT_NATIVE_ABI,
        amountInMax: amountIn,
        amountNATIVEOut: amountOut,
      }, // tokensForExactNative
    ],
  },
})
```
{% endcode %}
