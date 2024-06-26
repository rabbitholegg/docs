# Select the Reward

To incentivize your target recipients to transact, you must select the ERC20 token you’d like to reward users with. Start by selecting the network you want users to receive the token on. Boost currently supports the following networks for token rewards:

* Arbitrum
* Base
* Ethereum
* Optimism
* Polygon

{% hint style="info" %}
Note that the network the token is on can be different than the network the onchain action is set on in step 1.
{% endhint %}

After selecting the network, pick the token for rewarding users. Choose from the preset list of tokens, or choose '**Other**' to input a custom token. Ensure the correct network is chosen and enter the token address in the provided field.&#x20;

<figure><img src="../../.gitbook/assets/Deploy Boost - Boost Manager.jpeg" alt=""><figcaption></figcaption></figure>

After selecting the token, input the **total amount of tokens** you’d like to allocate to the boost. You will then have to select how much tokens you’d like to reward to each user that completes a boost transaction. This will determine how many boosts can be distributed, or in other words, how many users can receive the boost reward.

{% hint style="info" %}
One of the key benefits of Boost is that you can deploy boosts with as little as a cent. This completely lowers the barrier to implement with incentive distribution strategies by providing a platform to experiment and iterate with low overhead.
{% endhint %}

<figure><img src="../../.gitbook/assets/Deploy Boost - Boost Manager · 9.56am · 04-02.jpeg" alt=""><figcaption></figcaption></figure>

You have three options on how to select a reward amount per user:

* **Gas rebate:** a recommended amount that will cover the cost of gas for the user to complete the boost
* **Recommended:** a recommended amount based on previous boost data with similar attributes.
* **Custom:** input your own custom reward amount.

Selecting the reward amount is critical to the success of the boost. If you choose a low reward amount, users may not complete the boost transaction due to high gas costs. If you choose too high of a reward with poor audience targeting, you risk reaching the wrong users.
