---
description: Numerical Operators help with number comparisons.
---

# Numerical Operators

{% hint style="info" %}
You can use the helper functions as shown in the examples below instead of directly using the numerical operators. Using these functions in combination with viem's `parseEther` makes it much easier to work with amounts.
{% endhint %}

* **$gte:** for greater than or equals to comparisons

```javascript
import { parseEther } from 'viem'
import { GreaterThanOrEquals } from '@rabbitholegg/questdk'

const amountFilter = GreaterThanOrEquals(parseEther('0.1'))
// equivalent to { $gte: 100000000000000000 }
```

* **$gt:** for greater than comparisons

```javascript
import { parseEther } from 'viem'
import { GreaterThan } from '@rabbitholegg/questdk'

const amountFilter = GreaterThan(parseEther('0.1'))
// equivalent to { $gt: 100000000000000000 }
```

* **$lte:** for less than or equals to comparisons

```javascript
import { parseEther } from 'viem'
import { LessThanOrEquals } from '@rabbitholegg/questdk'

const amountFilter = LessThanOrEquals(parseEther('0.1'))
// equivalent to { $lte: 100000000000000000 }
```

* **$lt:** for less than comparisons

```javascript
import { parseEther } from 'viem'
import { LessThan } from '@rabbitholegg/questdk'

const amountFilter = LessThan(parseEther('0.1'))
// equivalent to { $lt: 100000000000000000 }
```

* **$eq:** for exact equality comparisons

```javascript
import { parseEther } from 'viem'
import { Equal } from '@rabbitholegg/questdk'

const amountFilter = Equal(parseEther('0.1'))
// equivalent to { $eq: 100000000000000000 }
```

{% hint style="info" %}
For exact quality comparisons, you can omit using `Equal`and just compare the value directly (ie: `parseEther('0.1')`).&#x20;
{% endhint %}
