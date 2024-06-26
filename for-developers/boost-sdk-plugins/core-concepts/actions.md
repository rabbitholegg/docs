# Actions

Actions are a core concept to plugins. Each action will have a standard set of parameters and is meant to encompass a common blockchain action like swap, mint, bridge or deposit. This standardization allows frontends like RabbitHole or Boost Inbox to dynamically request and display the appropriate parameters based on the selected action. For example, choosing 'swap' prompts the frontend to ask for swap parameters, while selecting 'bridge' leads to requesting bridge parameters

{% hint style="danger" %}
Avoid using inappropriate action types for different functionalities in your plugin. For example, don't use `MintActionParams` for staking actions. Matching the correct action type to its function is key to ensuring the plugin works as intended.
{% endhint %}

In this section we will teach you a few of the concepts related to actions.

### Action Types

When implementing your plugin, keep in mind the action type of the action you are wanting to support. In order for your action to be supported it needs to be one of the action types supported by [**questDK**](https://github.com/rabbitholegg/questdk).&#x20;

Here is a non-exhaustive list of some of the action types that can be supported by QuestDK Plugins

* swap
* bridge
* mint
* burn
* options
* delegate
* vote
* stake
* deposit
* lend

{% hint style="warning" %}
If the action type you want to make a plugin for is not available, [**please reach out to us on discord**](https://discord.gg/boost-protocol) to make a request for a new action type.
{% endhint %}

Each of these action types has a corresponding `ActionParams`. For example:

* [SwapActionParams](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/actions/types.ts#L5)
* [BridgeActionParams](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/actions/types.ts#L35)
* [MintActionParams](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/actions/types.ts#L44)
* [DelegateActionParams](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/actions/types.ts#L64)

These `ActionParams` each have a set of standard parameters that are specific to that action type.&#x20;

***

### ActionParams

[**View on Github**](https://github.com/rabbitholegg/questdk/blob/main/src/actions/types.ts)

ActionParams are standard sets of parameters which are specific to a certain action type. These are the parameters we expect the majority of transactions utilizing a certain action type to have. Swaps for example will all have parameters for the tokens and amounts used, and a mint action will have parameters for the mint contract address and tokenId.

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

{% hint style="success" %}
Check out the [**Types**](types.md) page to see the definitions of other `ActionParams`
{% endhint %}

You will want to map the parameters from the transactions inputs to these standard action params which are used by Boost Protocol. You can see an example of this [here](../building-your-plugin/implementing-the-transaction-filter.md#mapping-the-transaction-details-with-the-swapactionparams) in the plugin development guide.

***
