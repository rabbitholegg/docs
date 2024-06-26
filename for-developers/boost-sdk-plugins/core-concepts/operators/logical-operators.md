---
description: >-
  Understand how $and and $or are used to combine multiple conditions in plugin
  filters.
---

# Logical Operators

### `$and` Operator <a href="#and-operator" id="and-operator"></a>

**Purpose**: The `$and` operator is used to apply a set of filters and return `true` only if all filters are passed. It embodies the logical AND operation.

**Usage**: Used when all conditions need to be met simultaneously.&#x20;

**Example:** In the following example from the Uniswap plugin, the `$and` operator is used alongside the `$regex` operator to extract token addresses from a concatenated string of addresses and other identifiers.&#x20;

`0xda10009cbd5d07dd0cecc66161fc93d7c9000da11f44200000000000000000000000000000000000006`

{% code title="Uniswap.test.ts" %}
```javascript
{
  path: {
    $and: [
      {
        $regex: '^0xda10009cbd5d07dd0cecc66161fc93d7c9000da1', // DAI
      },
      {
        $regex: '4200000000000000000000000000000000000006$', // WETH
      },
    ],
  },
}
```
{% endcode %}

### `$or` Operator <a href="#and-operator" id="and-operator"></a>

**Purpose**: The `$or` operator is used to apply a set of filters and return `true` if any one of the filters passes, representing the logical OR operation.

**Usage**: The `$or` operator is useful when you want to pass the overall condition if any one of multiple conditions is met. This will often be used when a transaction can be routed through one of multiple contracts. (ie: aggregators)

**Example:** In the following example from the Connext plugin, the `$or` operator is used to allow transactions that interact with either contract to pass the filter. Each contract address will be compared to the `to` parameter of the transaction, and will pass if either one matches.

{% code title="Connext.ts" %}
```typescript
{
  to: {
    $or: [
      xcallContractAddress.toLowerCase(),
      multiSendContractAddress.toLowerCase(),
    ],
  },
}
```
{% endcode %}
