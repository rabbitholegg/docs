# ABI and Contracts

Before starting plugin development, it is important to identify the target contracts and the specific transactions to filter. The aim is to encompass all possible scenarios encountered when interacting with the project for which the plugin is being developed. The focus is on enhancing user experience by minimizing false negatives and ensuring the plugin covers a wide range of potential use cases.

For things like contract addresses and ABIs, try to use available SDKs or APIs to bring these values in programatically, otherwise they will need to be tracked down so we can use them during development.&#x20;

This step outlines the key elements needed for plugin development:

* Identifying contract addresses from where transactions originate.
* Acquiring the ABI for the transaction data you want to decode.
* Compiling a list of tokens your plugin will support, with an option to use a [default list of tokens for supported chains, which can be imported from the utils package](../core-concepts/utilities/constants.md#object-chain\_to\_tokens).  (only applicable to ERC-20 based actions such as swap, bridge and stake)

***

#### Find the Contract Addresses and ABI

Lets use Balancer as an example. On Balancer, all swap transactions are routed through the [Balancer Vault Contract](https://arbiscan.io/address/0xba12222222228d8ba445958a75a0704d566bf2c8#code), which has the same address on every chain. `0xBA12222222228d8Ba445958a75a0704d566BF2C8`.&#x20;

{% hint style="info" %}
If your projects contract has a different address on each chain, you will need to create a mapping of chains to contract addresses as seen [**here**](https://github.com/rabbitholegg/questdk-plugins/blob/fd797855c78239c1197145a2fb50fa9ceb648e43/packages/woofi/src/contract-addresses.ts#L4).&#x20;
{% endhint %}

{% code title="constants.ts" %}
```typescript
export const BALANCER_VAULT = '0xBA12222222228d8Ba445958a75a0704d566BF2C8'
```
{% endcode %}

Next step is to get the ABI for the transaction parameters you wish to decode. You can find the ABI by going to [contract page on Etherscan](https://arbiscan.io/address/0xba12222222228d8ba445958a75a0704d566bf2c8#code) and scrolling to the bottom to find the Contract ABI section.

{% hint style="info" %}
If the contract you are working with is a proxy, you may have to search for the implementation contract to get the correct abi. Most of the time you can find the implementation contract by using [this proxy checker tool](https://arbiscan.io/proxyContractChecker) on Etherscan.
{% endhint %}

Create a file called `constants.ts` to export the ABI fragments and contract addresses from. You have the option to compile all ABI fragments into a single constant or separate them into individual constants. Both methods are acceptable and depend on your preference or the specific needs of your project.

<pre class="language-typescript" data-title="constants.ts"><code class="lang-typescript">export const BALANCER_ABI = [
<strong>  {
</strong>    inputs: [
      {
        components: [
          {
            internalType: 'bytes32',
            name: 'poolId',
            type: 'bytes32',
          },
          {
            internalType: 'enum IVault.SwapKind',
            name: 'kind',
            type: 'uint8',
          },
          {
            internalType: 'contract IAsset',
            name: 'assetIn',
            type: 'address',
          },
          {
            internalType: 'contract IAsset',
            name: 'assetOut',
            type: 'address',
          },
          {
            internalType: 'uint256',
            name: 'amount',
            type: 'uint256',
          },
          {
            internalType: 'bytes',
            name: 'userData',
            type: 'bytes',
          },
        ],
        internalType: 'struct IVault.SingleSwap',
        name: 'singleSwap',
        type: 'tuple',
      },
      {
        components: [
          {
            internalType: 'address',
            name: 'sender',
            type: 'address',
          },
          {
            internalType: 'bool',
            name: 'fromInternalBalance',
            type: 'bool',
          },
          {
            internalType: 'address payable',
            name: 'recipient',
            type: 'address',
          },
          {
            internalType: 'bool',
            name: 'toInternalBalance',
            type: 'bool',
          },
        ],
        internalType: 'struct IVault.FundManagement',
        name: 'funds',
        type: 'tuple',
      },
      {
        internalType: 'uint256',
        name: 'limit',
        type: 'uint256',
      },
      {
        internalType: 'uint256',
        name: 'deadline',
        type: 'uint256',
      },
    ],
    name: 'swap',
    outputs: [
      {
        internalType: 'uint256',
        name: 'amountCalculated',
        type: 'uint256',
      },
    ],
    stateMutability: 'payable',
    type: 'function',
  },
]
</code></pre>

{% hint style="warning" %}
Always default to using a projects tooling, such as SDKs or other packages that you can use to get the current contract addresses and ABI. This is especially important if the project migrates or updates their contracts often.
{% endhint %}

Now we can import these constants into the main `Project.ts` file and we can start to implement the transaction filter.
