# Testing

For plugin development, we've adopted a Test-Driven Development (TDD) approach. This strategy involves initially writing unit tests for the plugin’s functionalities. This proactive step is aimed at minimizing bugs and ensuring a smooth development process.

***

{% hint style="success" %}
You can automatically generate test cases for your plugin by using our [**CLI Plugin Builder tool**](../building-your-plugin/#plugin-builder-cli-tool)**.**
{% endhint %}

### How to Manually create test cases for your plugin

After setting up your project with the CLI Builder tool, look for a file named `test-transactions.ts` in your projects folder. Open it and you will see a sample `TestParams` object which will be used as a template, and some arrays called `passingTestCases` and `failingTestCases`.

{% code title="test-transactions.ts" %}
```typescript
import { type SwapActionParams } from '@rabbitholegg/questdk'
import {
  createTestCase,
  type TestParams,
} from '@rabbitholegg/questdk-plugin-utils'

// values are placeholders, replace with actual values from your test transaction
export const SWAP_TEST: TestParams<MintActionParams> = {
  transaction: {
    chainId: 1,
    from: '0x0',
    hash: '0x0',
    input: '0x0',
    to: '0x0',
    value: '0',
  },
  params: {
    chainId: 0,
  },
}

export const passingTestCases = [
  createTestCase(SWAP_TEST, 'this is a demo test'),
]

export const failingTestCases = [
  createTestCase(SWAP_TEST, 'when chainId is not correct', { chainId: 99 }),
]
```
{% endcode %}

We want to replace the transaction parameters in `SWAP_TEST` with the parameters from an actual transaction. The best way to grab the parameters is to lookup the transaction hash on tenderly and copy the values over from the tenderly explorer.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-03-09 at 12.45.25@2x.png" alt=""><figcaption><p>You can easily find and copy the chain, hash, value, from, to and input parameters from tenderly explorer. This method is much more convenient than using etherscan.</p></figcaption></figure>

Or you can use this [**Transaction Fetcher Tool**](https://plugin-transaction-fetcher.onrender.com/) which will get all the parameters you need from the transaction. Just copy the output and paste it into the transaction object.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-03-09 at 12.49.26@2x.png" alt="" width="563"><figcaption><p>This transaction fetcher tool returns the needed parameters from a transaction.</p></figcaption></figure>

After pasting in the transaction details, your `test-transaction.ts` file will now look like this:

{% code title="test-transactions.ts" %}
```typescript
import { type SwapActionParams } from '@rabbitholegg/questdk'
import {
  createTestCase,
  type TestParams,
} from '@rabbitholegg/questdk-plugin-utils'

export const SWAP_TEST: TestParams<MintActionParams> = {
  transaction: {
    chainId: 42161,
    from: '0xcdd37ada79f589c15bd4f8fd2083dc88e34a2af2',
    to: '0xdef171fe48cf0115b1d80b88dc8eab59176fee57',
    hash: '0xf031ddefbb6f4a441de1b127b956285871a44419948fa3b27ec3bc5392b81d5b',
    input:
      '0x54e3f31b0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000fd086bc7cd5c481dcc9c85ebe478a1c0b69fcbb9000000000000000000000000ff970a61a04b1ca14834a43f5de4533ebddb5cc8000000000000000000000000000000000000000000000000000000001443fd00000000000000000000000000000000000000000000000000000000001429be4c000000000000000000000000000000000000000000000000000000001443ae8700000000000000000000000000000000000000000000000000000000000001e00000000000000000000000000000000000000000000000000000000000000220000000000000000000000000000000000000000000000000000000000000038000000000000000000000000000000000000000000000000000000000000003e0000000000000000000000000cdd37ada79f589c15bd4f8fd2083dc88e34a2af2000000000000000000000000e9290c80b28db1b3d9853ab1ee60c6630b87f57e0100000000000000000000000000000000000000000000000000000000004032000000000000000000000000000000000000000000000000000000000000042000000000000000000000000000000000000000000000000000000000651e25f17fc6bc6c3c404602ad4d5307c59743a50000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000010000000000000000000000001f721e2e82f6676fce4ea07a5958cf098d339e180000000000000000000000000000000000000000000000000000000000000124c04b8d59000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000def171fe48cf0115b1d80b88dc8eab59176fee570000000000000000000000000000000000000000000000000000000065270c11000000000000000000000000000000000000000000000000000000001443fd0000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000028fd086bc7cd5c481dcc9c85ebe478a1c0b69fcbb9ff970a61a04b1ca14834a43f5de4533ebddb5cc800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000124000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000',
    value: '0',
  },
  params: {
    chainId: 0,
  },
}

export const passingTestCases = [
  createTestCase(SWAP_TEST, 'this is a demo test'),
]

export const failingTestCases = [
  createTestCase(SWAP_TEST, 'when chainId is not correct', { chainId: 99 }),
]
```
{% endcode %}

Next step is to fill in the expected `params` for this transaction. We will need to fill in the expected `chainId`, `tokenIn`, `tokenOut`, `amountIn`, `amountOut` and `recipient`. If you are unsure of what these params should be for a given transaction, you can find this information on Tenderly explorer.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-03-09 at 12.55.10@2x.png" alt=""><figcaption><p>You can grab the params like amounts and tokens from tenderly. Take note of the decimals used for the token. USDC and USDT use 6 decimal places, so take that into account when doing comparisons.</p></figcaption></figure>

{% hint style="danger" %}
Amounts are sometimes subject to other factors like slippage settings that may cause the amount found in the transactions input data to be lower than what was actually received by the person swapping.
{% endhint %}

{% code title="test-transactions.ts" %}
```typescript
export const SWAP_TEST: TestParams<MintActionParams> = {
  transaction: {
    chainId: 42161,
    from: '0xcdd37ada79f589c15bd4f8fd2083dc88e34a2af2',
    to: '0xdef171fe48cf0115b1d80b88dc8eab59176fee57',
    hash: '0xf031ddefbb6f4a441de1b127b956285871a44419948fa3b27ec3bc5392b81d5b',
    input:
      '0x54e3f31b0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000fd086bc7cd5c481dcc9c85ebe478a1c0b69fcbb9000000000000000000000000ff970a61a04b1ca14834a43f5de4533ebddb5cc8000000000000000000000000000000000000000000000000000000001443fd00000000000000000000000000000000000000000000000000000000001429be4c000000000000000000000000000000000000000000000000000000001443ae8700000000000000000000000000000000000000000000000000000000000001e00000000000000000000000000000000000000000000000000000000000000220000000000000000000000000000000000000000000000000000000000000038000000000000000000000000000000000000000000000000000000000000003e0000000000000000000000000cdd37ada79f589c15bd4f8fd2083dc88e34a2af2000000000000000000000000e9290c80b28db1b3d9853ab1ee60c6630b87f57e0100000000000000000000000000000000000000000000000000000000004032000000000000000000000000000000000000000000000000000000000000042000000000000000000000000000000000000000000000000000000000651e25f17fc6bc6c3c404602ad4d5307c59743a50000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000010000000000000000000000001f721e2e82f6676fce4ea07a5958cf098d339e180000000000000000000000000000000000000000000000000000000000000124c04b8d59000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000def171fe48cf0115b1d80b88dc8eab59176fee570000000000000000000000000000000000000000000000000000000065270c11000000000000000000000000000000000000000000000000000000001443fd0000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000028fd086bc7cd5c481dcc9c85ebe478a1c0b69fcbb9ff970a61a04b1ca14834a43f5de4533ebddb5cc800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000124000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000',
    value: '0',
  },
  params: {
    chainId: Chains.ARBITRUM_ONE,
    tokenIn: '0xfd086bc7cd5c481dcc9c85ebe478a1c0b69fcbb9', // USDT
    tokenOut: '0xff970a61a04b1ca14834a43f5de4533ebddb5cc8', // USDC.e
    amountIn: GreaterThanOrEqual(parseUnits('330', 6)), // decimals set to 6
    amountOut: GreaterThanOrEqual(parseUnits('330', 6)), // decimals set to 6
    recipient: '0x815ac0ccf85bab38b1953a008f80bb028bfc317a',
  },
}
```
{% endcode %}

Once you have provided both the `transaction`, and the `params` to the `TestParams` object, we can use it to create tests using the built-in [`createTestCase`](utilities/helpers.md#function-createtestcase) utility function. Create a [`TestCase`](https://github.com/rabbitholegg/questdk-plugins/blob/262b99cb5d797f51fdf06145a74a0ebc717bc0f3/packages/utils/src/helpers/test-helpers.ts#L14) for your `SWAP_TEST` and replace the sample transaction description that is in the `passingTestCases` array.

```typescript
// these tests are expected to pass
export const passingTestCases = [
  createTestCase(SWAP_TEST, 'when using the simpleSwap function'),
]
```

{% hint style="info" %}
The test case arrays`passingTestCases` and `failingTestCases`are imported into your`Project.test.ts` file where the test cases are then executed.
{% endhint %}

Repeat this process for each contract method a transaction may use. It's important to have a dedicated test case for every distinct scenario. In the case of Paraswap, this includes testing various swap functions like simple swap, multiswap, uniV3 swap, etc., to ensure comprehensive coverage of all possible use cases.

```typescript
// these tests are expected to pass
export const passingTestCases = [
  createTestCase(SIMPLE_SWAP, 'when using simpleSwap function'),
  createTestCase(MULTI_SWAP, 'when using multiSwap function'),
  createTestCase(MEGA_SWAP, 'when using megaSwap function'),
  createTestCase(UNIV3_SWAP, 'when using univ3Swap function'),
]
```

After establishing successful test cases, it's important to also add tests that are expected to fail. These tests verify that transactions not meeting certain criteria, such as amount, token, or chain, indeed fail as expected. For example, a transaction with a value of 0.5 ETH should fail a filter set for transactions with a value over 1 ETH. To conduct these tests, use the `override` argument in the [`createTestCase`](https://github.com/rabbitholegg/questdk-plugins/blob/262b99cb5d797f51fdf06145a74a0ebc717bc0f3/packages/utils/src/helpers/test-helpers.ts#L38) function. This lets you modify specific parameters in the `TestParams` object, ensuring the filters correctly reject transactions that don't align with the defined conditions. `override` is the third argument for the `createTestCase` function. You can see how it is used below to override the token and amount parameters with values that are expected to fail.

```typescript
// these tests are expected to fail
export const failingTestCases = [
  createTestCase(SIMPLE_SWAP, 'when amountIn is not sufficient', {
    amountIn: GreaterThanOrEqual(parseUnits('1000000', 6)), 
  }),
  createTestCase(MULTI_SWAP, 'when amountOut is not sufficient', {
    amountOut: GreaterThanOrEqual(parseUnits('1000000', 6)),
  }),
  createTestCase(MEGA_SWAP, 'when tokenIn is not correct', {
    tokenIn: '0xDA10009cBd5D07dd0CeCc66161FC93D7c9000da1', // DAI
  }),
  createTestCase(UNIV3_SWAP, 'when tokenOut is not correct', {
    tokenOut: '0xaf88d065e77c8cc2239327c5edb3a432268e5831', // USDC
  }),
]
```

***
