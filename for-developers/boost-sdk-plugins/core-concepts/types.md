# Types

### type `SwapActionParams`

**Description:** Defines parameters for swap-related actions.&#x20;

**Properties:**

* `chainId`: <mark style="color:yellow;">`Number`</mark>, specifies the chain ID.
* `contractAddress`: <mark style="color:yellow;">`Address`</mark> (optional), the address of the contract involved in the swap.
* `tokenIn`: <mark style="color:yellow;">`Address`</mark> (optional), address of the input token.
* `tokenOut`: `Address` (optional), address of the output token.
* `amountIn`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), the input amount for the swap.
* `amountOut`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), the output amount from the swap.
* `recipient`: `Address` (optional), the address receiving the output of the swap.
* `deadline`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), the deadline by which the swap must occur.

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

***

### type `OptionsActionParams`

**Description:** Specifies parameters for options-related actions.&#x20;

**Properties:**

* `chainId`: <mark style="color:yellow;">`Number`</mark>, identifies the chain ID.
* `contractAddress`: <mark style="color:yellow;">`Address`</mark> (optional), address of the contract involved.
* `token`: <mark style="color:yellow;">`Address`</mark> (optional), token address involved in the option.
* `amount`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), amount involved in the option.
* `recipient`: <mark style="color:yellow;">`Address`</mark> (optional), recipient address.
* `orderType`: [`OrderType`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/actions/types.ts#L128) (optional), specifies the type of order (e.g., limit, market).

```typescript
type OptionsActionParams = {
  chainId: number
  contractAddress?: Address
  token?: Address
  amount?: bigint | FilterOperator
  recipient?: Address
  orderType?: OrderType
}
```

***

### type `StakeActionParams`

**Description:** Defines parameters for staking actions.&#x20;

**Properties:**

* `chainId`: <mark style="color:yellow;">`Number`</mark>, specifies the chain ID.
* `contractAddress`: <mark style="color:yellow;">`Address`</mark> (optional), address of the contract involved.
* `tokenOne`: <mark style="color:yellow;">`Address`</mark> (optional), first token's address used in staking.
* `amountOne`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), amount of the first token staked.
* `tokenTwo`: <mark style="color:yellow;">`Address`</mark> (optional), second token's address used in staking.
* `amountTwo`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), amount of the second token staked.
* `duration`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), the duration of the staking.

```typescript
type StakeActionParams = {
  chainId: number
  contractAddress?: Address
  tokenOne?: Address
  amountOne?: bigint | FilterOperator
  tokenTwo?: Address
  amountTwo?: bigint | FilterOperator
  duration?: bigint | FilterOperator
}
```

***

### type `BridgeActionParams`

**Description:** Parameters for bridge action between chains.&#x20;

**Properties:**

* `sourceChainId`: <mark style="color:yellow;">`Number`</mark>, identifies the source chain ID.
* `destinationChainId`: <mark style="color:yellow;">`Number`</mark>, identifies the destination chain ID.
* `contractAddress`: <mark style="color:yellow;">`Address`</mark> (optional), the contract's address used for bridging.
* `tokenAddress`: <mark style="color:yellow;">`Address`</mark> (optional), the token's address being bridged.
* `amount`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), amount of the token being bridged.
* `recipient`: <mark style="color:yellow;">`Address`</mark> (optional), recipient's address on the destination chain.

```typescript
type BridgeActionParams = {
  sourceChainId: number
  destinationChainId: number
  contractAddress?: Address
  tokenAddress?: Address
  amount?: bigint | FilterOperator
  recipient?: Address
}
```

***

### type `MintActionParams`

**Description:** Parameters for minting actions in transactions.&#x20;

**Properties:**

* `chainId`: <mark style="color:yellow;">`Number`</mark>, indicates the chain ID where minting occurs.
* `contractAddress`: <mark style="color:yellow;">`Address`</mark>, the contract's address for minting operations.
* `tokenId`: <mark style="color:yellow;">`Number`</mark> (optional), identifies the specific token to be minted.
* `amount`: <mark style="color:yellow;">`Number`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), quantity of tokens to mint.
* `recipient`: <mark style="color:yellow;">`Address`</mark> (optional), address receiving the minted tokens.

```typescript
type MintActionParams = {
  chainId: number
  contractAddress: Address
  tokenId?: number
  amount?: number | FilterOperator
  recipient?: Address
}
```

***

### type `BurnActionParams`

**Description:** Describes parameters for burn actions, often mirroring mint parameters. **Properties:**

* Same as `MintActionParams.`Used for removing tokens from circulation.

```typescript
type BurnActionParams = MintActionParam
```

***

### type `QuestActionParams`

**Description:** Specifies parameters for actions related to quests.&#x20;

**Properties:**

* `chainId`: <mark style="color:yellow;">`Number`</mark>, the chain ID relevant to the quest.
* `rewardToken`: <mark style="color:yellow;">`Address`</mark> (optional), token address used as a reward.
* `rewardAmount`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), amount of the reward token.
* `startTime`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), quest start time.
* `endTime`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), quest end time.
* `totalParticipants`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), number of participants.
* `actionSpec`: <mark style="color:yellow;">`String`</mark> (optional), specifies the action criteria for the quest.

```typescript
type QuestActionParams = {
  chainId: number
  rewardToken?: Address
  rewardAmount?: bigint | FilterOperator
  startTime?: bigint | FilterOperator
  endTime?: bigint | FilterOperator
  totalParticipants?: bigint | FilterOperator
  actionSpec?: string
}
```

***

### type `DelegateActionParams`

**Description:** Details parameters for delegation actions.&#x20;

**Properties:**

* `chainId`: <mark style="color:yellow;">`Number`</mark>,  the chain ID relevant to the delegate action.
* `delegate`: <mark style="color:yellow;">`Address`</mark> (optional), address of the delegate.
* `project`: <mark style="color:yellow;">`Address`</mark> or String, project address or identifier for delegation.
* `contractAddress`: <mark style="color:yellow;">`Address`</mark> (optional), associated contract's address.
* `amount`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L43) (optional), amount being delegated.
* `delegator`: <mark style="color:yellow;">`Address`</mark> (optional), address of the delegator.

```typescript
type DelegateActionParams = {
  chainId: number
  delegate?: Address
  project: Address | string
  contractAddress?: Address
  amount?: bigint | FilterOperator
  delegator?: Address
}
```

***

### type `VoteActionParams`

**Description:** Details parameters for delegation actions.&#x20;

**Properties**:

* `chainId`: <mark style="color:yellow;">`Number`</mark>, the chain ID relevant to the voting action.
* `project`: <mark style="color:yellow;">`Address`</mark> or <mark style="color:yellow;">`String`</mark>, project address or identifier for the vote.
* `support?`: <mark style="color:yellow;">`BigInt`</mark>, <mark style="color:yellow;">`Boolean`</mark>, or [`FilterOperator`](types.md#type-filteroperator) (optional), indicates support for the proposal. Can represent a simple yes/no, a specific amount of support, or complex filtering conditions.
* `proposalId?`: <mark style="color:yellow;">`BigInt`</mark> or [`FilterOperator`](types.md#type-filteroperator) (optional), identifier for the proposal being voted on. Can represent a specific proposal ID or complex filtering conditions related to proposal IDs.

```typescript
type VoteActionParams = {
  chainId: number
  project: Address | string
  support?: bigint | boolean | FilterOperator
  proposalId?: bigint | FilterOperator
}
```

***

### type `ActionParams`

**Description:** A union type representing different action parameter structures.&#x20;

**Properties:**

* Represents a combination of different action parameter types, such as `SwapActionParams`, `StakeActionParams`, `BridgeActionParams`, `MintActionParams`, `DelegateActionParams`, `QuestActionParams`, and `OptionsActionParams`.
* Each variant within this union type caters to specific transaction types and contains properties relevant to that transaction.

```typescript
type ActionParams =
  | SwapActionParams
  | StakeActionParams
  | BridgeActionParams
  | MintActionParams
  | DelegateActionParams
  | QuestActionParams
  | OptionsActionParams
```

***

### type `IActionPlugin`

**Description:** Interface for action plugins in the system.&#x20;

**Properties:**

* `pluginId`: <mark style="color:yellow;">`String`</mark>, a unique identifier for the plugin.
* `getSupportedChainIds`: <mark style="color:orange;">`Function`</mark>, returns a list of supported blockchain IDs.
* `getSupportedTokenAddresses`: <mark style="color:orange;">`Function`</mark>, provides supported token addresses for a given chain.
* Methods: Includes various functions like `bridge`, `swap`, `mint`, each corresponding to different action types and returning either a [`TransactionFilter`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/filter/types.ts#L49) or a [`PluginActionNotImplementedError`](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/errors/plugin.ts#L1).

[**View on Github**](https://github.com/rabbitholegg/questdk/blob/3649c880ffc4da5d26fe8a5ebb7977346516376c/src/actions/types.ts#L81)

***

### enum `ActionType`

**Description:** Enum representing different types of available actions.&#x20;

**Properties:**

* Defines specific action types like `Bridge`, `Stake`, `Swap`, `Mint`, `Burn`, `Quest`, `Deposit`, `Delegate`, `Lend`, `Other`, and `Options`.
* Each value in this enum is a string that corresponds to a specific action type.

```typescript
enum ActionType {
  Bridge = 'bridge',
  Stake = 'stake',
  Swap = 'swap',
  Mint = 'mint',
  Burn = 'burn',
  Quest = 'quest',
  Deposit = 'deposit',
  Delegate = 'delegate',
  Lend = 'lend',
  Other = 'other',
  Options = 'options',
}
```

***

### type `OrderType`

**Description:** Enum for defining order types in options/derivatives transactions.

**Properties:**

* `Limit`: Represents a limit order type.
* `Market`: Represents a market order type.

```typescript
enum OrderType {
  Limit = 'limit',
  Market = 'market',
}
```

***

### type `ArrayOperator`

**Description**: Represents operations that can be performed on arrays within filters.

```typescript
type ArrayOperator =
  | {
      $some?: FilterOperator[]
    }
  | {
      $first?: FilterOperator
    }
  | {
      $last?: FilterOperator
    }
  | {
      $nth?: NthFilter
    }
```

***

### type `LogicalOperator`

**Description**: Defines logical operations for combining multiple filter criteria.

```typescript
type LogicalOperator =
  | {
      $and?: FilterOperator[]
    }
  | {
      $or?: FilterOperator[]
    }
```

***

### type `NumericOperator`

**Description**: Specifies numerical operations for filtering.

```typescript
type NumericOperator =
  | bigint
  | number
  | string
  | {
      $gt?: bigint
    }
  | {
      $gte?: bigint
    }
  | {
      $lt?: bigint
    }
  | {
      $lte?: bigint
    }
```

***

### type `StringOperator`

**Description**: Defines string operations for filtering, using regular expressions.

**Properties**:

* `$regex?`: A regular expression string for matching.

```typescript
type StringOperator = {
  $regex?: string
}
```

***

### type `FilterOperator`

**Description**: A union type that encompasses various filtering operations, including logical, numeric, array, and string operations.

```typescript
type FilterOperator =
  | LogicalOperator
  | NumericOperator
  | ArrayOperator
  | StringOperator
```

***

### type `TransactionFilter`

**Description**: Represents a filter applied to transactions, where each property of a transaction can be filtered using a `FilterOperator`.

```typescript
type TransactionFilter = {
  [K in keyof Transaction]: FilterOperator
}
```

***

### type `FilterObject`

**Description**: An object representing a complex filter structure, where each key corresponds to a condition defined by the `Filter` type.

```typescript
type FilterObject = {
  [key: string]: Filter
}
```

***

### type `BitmaskFilter`

**Description**: Allows filtering based on bitmask operations.

**Properties**:

* `bitmask`: The bitmask value, which can be a `bigint`, `number`, or `string`.
* `value`: The value to compare against the bitmask, can be a `bigint`, `number`, `string`, or `NumericOperator`.

<pre class="language-typescript"><code class="lang-typescript"><strong>type BitmaskFilter = {
</strong>  bitmask: bigint | number | string
  value: bigint | number | string | NumericOperator
}
</code></pre>

***

### type `NthFilter`

**Description**: Specifies a filter to apply to the nth element of an array.

**Properties**:

* `index`: The index of the element to apply the filter to, can be a `bigint`, `number`, or `string`.
* `value`: The filter to apply, can be either a `TransactionFilter` or a `FilterObject`.

```typescript
type NthFilter = {
  index: bigint | number | string
  value: TransactionFilter | FilterObject
}
```

***

### type `Filter`

**Description**: Represents the base type for filters, which can be a primitive value, a `FilterObject`, a filter array, or an ABI type.

```typescript
type Filter = Primitive | FilterObject | FilterArray | Abi
```
