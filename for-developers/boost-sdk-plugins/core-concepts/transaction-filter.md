# Transaction Filter

The Transaction Filter is the heart of the plugin and is where all the logic for filtering transactions should go. Go into your `[Project].ts` file in the `src` folder of your project. \
You will see a function named for the action type (ie: `swap`) you selected in the [**CLI builder**](../building-your-plugin/#plugin-builder-cli-tool). This function creates and returns the transaction filter which will be used to determine which transactions are considered valid.

{% code title="Project.ts" %}
```typescript
export const swap = async (
  swap: SwapActionParams,
): Promise<TransactionFilter> => {
 
  const { chainId, contractAddress, tokenIn } = swap

  return compressJson({
    chainId, 
    to: '0x0',
    input: {}, 
  })
}
```
{% endcode %}

When implementing the transaction filter function, the parameters coming in are the criteria set when creating a boost in boost terminal. Lets use the Across `bridge` plugin as an example:

<pre class="language-typescript" data-title="Across.ts" data-overflow="wrap"><code class="lang-typescript">import { type BridgeActionParams, compressJson } from '@rabbitholegg/questdk'
import { type Address } from 'viem'
import { CHAIN_ID_ARRAY } from './chain-ids.js'
import { ACROSS_BRIDGE_ABI } from './abi.js'
import { CHAIN_TO_CONTRACT } from './chain-to-contract.js'

export const bridge = async (bridge: BridgeActionParams) => {
  // This is the information we'll use to compose the Transaction object
<strong>  const { sourceChainId, destinationChainId, tokenAddress, amount, recipient } = bridge
</strong></code></pre>

The incoming parameters will be based on the action type used, and the specific `ActionParams` available to that action type. We have to map these supplied expected values against the actual ABI of the transaction we’ll be parsing:

```typescript
return compressJson({
    chainId: sourceChainId, // The chainId of the source chain
    to: contractAddress, // The contract address of the bridge
    input: {
      $abi: ACROSS_BRIDGE_ABI, // The ABI of the bridge contract
      recipient, // The recipient of the funds
      destinationChainId, // The chainId of the destination chain
      amount, // The amount of tokens to send
      originToken: tokenAddress, // The token address of the token to send
    }, // The input object is where we'll put the ABI and the parameters
  })
```

<figure><img src="../../../.gitbook/assets/CleanShot 2024-03-09 at 14.30.30@2x.png" alt=""><figcaption><p>We match the inputs of the transaction with the standard <code>BridgeActionParams</code></p></figcaption></figure>

The `chainId` and `to` parameters in the example `bridge` function both map directly to these params on the transaction object, which are `transaction.to` and `transaction.chainId`. Any param on the transaction object can be used in your filter (`transaction.from` is useful for matching to the `recipient`). For the input object you need to supply an ABI that contains the function signature of the relevant function. This can be a modified ABI that holds the function signature of multiple contracts. The filter will correctly pull out the one with the right signature. The keys of the JSON object (i.e `originToken` ) needs to key into the expected value based on the parameters passed in from the action (`tokenAddress`).\
\
This function will return a [`TransactionFilter`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L49) object, which will contain the parameters that will be used to determine if a certain transaction is valid.
