# Constants

## enum `Chains`

[**View on Github**](https://github.com/rabbitholegg/questdk-plugins/blob/fd797855c78239c1197145a2fb50fa9ceb648e43/packages/utils/src/constants/contract-addresses.ts#L68)

**Purpose:** The `Chains` enum contains the chain ids for all the chains supported by Boost Protocol. It is recommended to use this enum whenever possible to ensure the correct chainId is being used.

**Import**

```javascript
import { Chains } from '@rabbitholegg/questdk-plugin-utils'
```

**Usage**

```javascript
const chainId = Chains.ETHEREUM // 1
```

***

## object `CHAIN_TO_TOKENS`

**Purpose:** The `CHAIN_TO_TOKENS` object maps chain IDs to arrays of token addresses relevant to each network. To see the full list of tokens for each chain, please see the github link below.

[**View on Github**](https://github.com/rabbitholegg/questdk-plugins/blob/fd797855c78239c1197145a2fb50fa9ceb648e43/packages/utils/src/constants/contract-addresses.ts#L68)

**Import**

```javascript
import { CHAIN_TO_TOKENS, Chains } from '@rabbitholegg/questdk-plugin-utils'
```

**Usage**

```javascript
const baseTokens = CHAIN_TO_TOKENS[Chains.BASE]
/* [
  ETH_ADDRESS, // ETH
  '0x4158734D47Fc9692176B5085E0F52ee0Da5d47F1', // BAL
  '0x2Ae3F1Ec7F1F5012CFEab0185bfc7aa3cf0DEc22', // cbETH
  '0x50c5725949A6F0c72E6C4a641F24049A917DB0Cb', // DAI
  '0xd9aAEc86B65D86f6A7B5B1b0c42FFA531710b6CA', // USDbC
  '0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913', // USDC
  '0x4200000000000000000000000000000000000006', // WETH
] */
```
