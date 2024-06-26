# Implementing the Transaction Filter

Now that our project is setup, the next step will be to implement the transaction filter. This is where we will map transaction data from an eligible transaction to standardized [ActionParams](../core-concepts/actions.md#actionparams) which are used by Boost Protocol. In the following example we will show you how to implement the transaction filter for a swap action on Balancer.

Head on over to your newly created \[Project].ts file. You will see a function with the name of the action type you selected. We can start by mapping the imported `BALANCER_VAULT` contract with the `to` parameter, and the `chainId` from the `SwapActionParams` to the `chainId` in the `TransactionFilter` object.

<pre class="language-typescript" data-title="[Project].ts"><code class="lang-typescript"><strong>import { BALANCER_VAULT } from './constants'
</strong>
export const swap = async (
  swap: SwapActionParams,
): Promise&#x3C;TransactionFilter> => {

  const { chainId } = swap

  return compressJson({
<strong>    chainId,
</strong><strong>    to: BALANCER_VAULT, 
</strong>    input: {},
  })
}
</code></pre>

Now lets look at this [swap transaction on Balancer](https://arbiscan.io/tx/0xe3540a63c3b6141dc5e3096a24f2d347c8abb72ef3ab0aeda54aec61faaba0d3).

<figure><img src="../../../.gitbook/assets/CleanShot 2024-03-06 at 12.49.16@2x.png" alt=""><figcaption><p>A swap made on Balancer</p></figcaption></figure>

We want to map the transaction details that are relevant to the swap action with the standardized Boost [SwapActionParams](../core-concepts/actions.md#swapactionparams). The SwapActionParams will be passed in by the boost creator and will need to match the details of the transaction in order to pass the filter.

```typescript
type SwapActionParams = {
  chainId: number
  contractAddress?: Address
  tokenIn?: Address
  tokenOut?: Address
  amountIn?: bigint | FilterOperator
  amountOut?: bigint | FilterOperator
  recipient?: Address
  deadline?: bigint | FilterOperator
}
```

#### **Mapping the transaction details with the SwapActionParams:**

* singleSwap.assetIn -> `tokenIn`
* singleSwap.assetOut -> `tokenOut`
* singleSwap.amount -> `amountIn`
* limit -> `amountOut` _(this value is the minimum amount of tokens received, so it may be less than the actual amount received in the transaction)_
* funds.recipient -> `recipient`

{% hint style="danger" %}
**Need help or have questions?** **Join the** [**Boost Protocol Discord**](https://discord.gg/boost-protocol)
{% endhint %}

Now that we know how to properly map the transaction details with the standard action params, we can start to implement the filter.

<pre class="language-typescript" data-title="Balancer.ts"><code class="lang-typescript">import { BALANCER_ABI, BALANCER_VAULT } from './constants'

export const swap = async (
  swap: SwapActionParams,
): Promise&#x3C;TransactionFilter> => {
  const {
    chainId,
    contractAddress,
    tokenIn,
    tokenOut,
    amountIn,
    amountOut,
    recipient,
  } = swap

  return compressJson({
    chainId: chainId,
    to: BALANCER_VAULT
    input: {
      $abi: BALANCER_ABI,
<strong>      singleSwap: {
</strong><strong>        assetIn: tokenIn,
</strong><strong>        assetOut: tokenOut,
</strong><strong>        amount: amountIn,
</strong><strong>      },
</strong><strong>      limit: amountOut,
</strong><strong>      funds: {
</strong><strong>        recipient: recipient,
</strong><strong>      },
</strong>    },
  })
}
</code></pre>

{% hint style="danger" %}
Please take note that not all parameters will map this easily together. It is often the case where the ActionParams need to be manipulated in some way to match the transaction inputs. For example, you may need to map tokens addresses to pools, or use one of the available [Operators](../core-concepts/operators/) to isolate the value inside of an array or string.
{% endhint %}

Once you have your transaction filter setup, we need to make sure it passes the unit tests that were setup during [the setup process](./#plugin-builder-cli-tool). Make sure to cover as many edge cases as you can while testing and cover all possible contract functions a valid transaction may use. To run the tests:

{% code title="terminal" %}
```bash
pnpm test --filter=@rabbitholegg/questdk-plugin-[project]
```
{% endcode %}

If you would like more in-depth information on how to manually setup additional test cases for your plugin please check out our page on testing.

{% content-ref url="../core-concepts/testing.md" %}
[testing.md](../core-concepts/testing.md)
{% endcontent-ref %}

If all the tests are passing, you are ready to move on to the final steps.
