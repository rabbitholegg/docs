---
description: How to claim a Boost for an end user
---

# Claim a Boost

Once an end user has completed a boosted action, the boost reward can be claimed by submitting a transaction signed by the end user on the chain of the reward token.

Prerequisites for claiming a boost include:

* the boost contract address (specific to each boost), which can be queried using [the boost details endpoint](fetch-boosts.md#querying-details-for-a-specific-boost) or found at `boost.contractAddress` in the response from [the create boost endpoint](create-a-boost.md#submitting-the-create-boost-request)
* the boost factory contract ABI, which can be found [here](https://github.com/rabbitholegg/questdk/blob/main/src/abi/quest-factory.ts)
* a signature from the Boost API vouching that a specific end user has completed the action for a currently active boost

### Getting a boost completion signature

Before submitting the claim transaction, a signature verifying the completion of the specific boost action by the end user must be requested from [the /boosts/get-signature endpoint](https://api.boost.xyz/docs#tag/boosts/paths/\~1boosts\~1get-signature/post).

<pre class="language-typescript"><code class="lang-typescript"><strong>const getSignatureResponse = await fetch('http://api.boost.xyz/boosts/get-signature', {
</strong>  method: 'POST',
  headers: {
    'Content-type': 'application/json',
  },
  body: JSON.stringify({
<strong>    boostId: 'c79de3f3-8741-4281-a1cb-4b6947e4060d',
</strong>    address: '0x242c295E88760559A6cA8E8F02bB52cdcF7f7422', // end-user address
  })
});

const { signature, compressedBytes, fee } = await getSignatureResponse.json();
</code></pre>

> While the raw `signature` is available in the response, the `compressedBytes` parameter of the response can be passed directly to the claim transaction below. Additionally, the required gas `fee` to claim the boost is available in the response for convenience.

### Claiming a boost reward

The following example demonstrates a claim of a reward in $DEGEN token on Base using the `viem` package and the `compressedBytes` param from the previous section:

```typescript
import { type WalletClient, type PublicClient } from 'viem';
import boostFactoryAbi from './abis/boostFactory';

async function claimBoostReward(
  publicClient: PublicClient,
  walletClient: WalletClient,
  boostContractAddress: string, // taken from GET /boosts/[boostId] response
  compressedBytes: string, // taken from POST /boosts/get-signature response
  fee: string, // taken from POST /boosts/get-signature response
) {
  const { request } = await publicClient.simulateContract({
    account: walletClient.account.address,
    address: boostContractAddress,
    abi: boostFactoryAbi,
    functionName: 'claimCompressed',
    args: [compressedBytes as Hex],
    value: BigInt(fee),
  });

  const txHash = await walletClient.writeContract(request);
}
```
