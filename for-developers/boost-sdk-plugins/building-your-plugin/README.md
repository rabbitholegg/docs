---
description: A step-by-step guide to building your first plugin
---

# Building Your Plugin

Before you start to build your plugin, make sure you first have a solid understanding of the core concepts like [**ABI Decoding**](../core-concepts/abi-decoding.md) and how to use the built-in [**Operators**](../core-concepts/operators/).

## Installation

**Requirements:**

* Node v20.11.0 LTS
* PNPM v.8.14.0 or higher

**Quick Start:**

Clone the repository and install dependencies&#x20;

{% code title="terminal" %}
```bash
git clone https://github.com/rabbitholegg/questdk-plugins.git
cd questdk-plugins
pnpm install
pnpm build
```
{% endcode %}

***

If you are planning to submit your plugin for review, please read our contribution guidelines.

{% content-ref url="../contribution-guidelines.md" %}
[contribution-guidelines.md](../contribution-guidelines.md)
{% endcontent-ref %}

***

### Plugin Builder CLI tool

To quickly get you started building your plugin, you can use the CLI plugin creation tool. It will ask you a series of questions based on the action type you want to use and it will automatically setup the project and test files for you. **To get the best results, please have some transaction hashes for the transactions you wish to recognize with your plugin, as well as some of the transaction details like token addresses and amounts if applicable.**

To start the plugin builder run this command from the root of questdk-plugins:

{% code title="terminal" %}
```bash
pnpm run create
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/CleanShot 2024-03-09 at 15.50.29@2x.png" alt="" width="563"><figcaption><p>The CLI Plugin Creator</p></figcaption></figure>

**Q. What is the name of the project you are creating a plugin for?**

Enter a name for your plugin project. Please use PascalCase or camelCase with no spaces, numbers or special characters (myProject, MyProject).&#x20;

**Q. What blockchains are the project on? (multi-select)**&#x20;

Select the action type that you wish to cover in your plugin. _(note: our plugin builder only supports using one action type at a time)_

_**Q.**_** Do you want to make this package public?**

Select _**"Yes"**_ if you want your plugin to be published to NPM, otherwise _**"No"**_.

**Q. Provide a transaction hash: (Optional)**

Optionally enter a transaction hash. If a transaction is found, it will continue to ask you more questions about the transaction based on what action type you have chosen. Repeat these steps for each transaction you wish to cover in your plugin.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-03-09 at 19.54.05@2x.png" alt="" width="563"><figcaption><p>If a transaction hash is provided, you will be asked additional questions about that<br> transaction based on the action type you selected.</p></figcaption></figure>

{% tabs %}
{% tab title="Mint" %}
**Q. If mint is ERC-1155, please enter the tokenId**

Optionally provide the tokenId if the mint is an ERC-1155 token. Skip this question if the mint is for an ERC-721 token.
{% endtab %}

{% tab title="Swap" %}
**Q. What is the contract address for tokenIn?**

Optionally provide a token address for the input token. For ETH and other native assets you can use the zero address. `0x0000000000000000000000000000000000000000`

**Q. What is the amount of tokens swapped?**

Provide the amount of tokens swapped. Make sure the value you use is `<=` to the actual amount of tokens swapped. This amount is used for testing purposes and will be applied with a function called `GreaterThanOrEquals`.

**Q. What is the contract address for tokenOut?**

Optionally provide a token address for the output token.
{% endtab %}

{% tab title="Bridge" %}
**Q. What is the destination chain?**

Select the destination chain for the bridge transaction from the dropdown.

**Q. What is the contract address for token being bridged?**

Optionally provide a token address for the input token. For ETH and other native assets you can use the zero address. `0x0000000000000000000000000000000000000000`

**Q. What is the amount of tokens being bridged?**

Provide the amount of tokens bridged. Make sure the value you use is `<=` to the actual amount of tokens bridged. This amount is used for testing purposes and will be applied with a function called `GreaterThanOrEquals`.
{% endtab %}

{% tab title="Stake" %}
**Q. What is the contract address for tokenOne?**

Optionally provide a token address for the tokenOne. For ETH and other native assets you can use the zero address. `0x0000000000000000000000000000000000000000`

**Q. What is the amount of tokenOne being staked?**

Provide the amount of tokens being staked. Make sure the value you use is `<=` to the actual amount of tokens staked. This amount is used for testing purposes and will be applied with a function called `GreaterThanOrEquals`.

**Q. What is the contract address for tokenTwo?**

**Q. What is the amount of tokenTwo being staked?**
{% endtab %}

{% tab title="Delegate" %}
**Q. What is the address of the delegate?**

Optionally provide the address the delegate that is receiving the voting power.

**Q. What is the project address?**

Optionally provide the address of the project or token that is being delegated. For Arbitrum DAO delegation, you would use the token address for ARB for example.

**Q. What is the amount of tokens being delegated?**

Provide the amount of tokens being delegated **in wei**. Make sure the value you use is `<=` to the actual amount of tokens delegated. This amount is used for testing purposes and will be applied with a function called `GreaterThanOrEquals`.

**Q. What is the address of the delegator?**

Optionally provide the address for the account that is delegating.
{% endtab %}

{% tab title="Options" %}
**Q. What is the contract address for the collateral token?**

Optionally provide a token address for the collateral token. For ETH and other native assets you can use the zero address. `0x0000000000000000000000000000000000000000`

**Q. What is the amount of collateral?**

Provide the amount of tokens that are provided as collateral for the trade. Make sure the value you use is `<=` to the actual amount of tokens provided as collateral. This amount is used for testing purposes and will be applied with a function called `GreaterThanOrEquals`.

**Q. What is the order type?**

Optionally provide the order type that was used in the transaction. This will either be "market" or "limit".
{% endtab %}
{% endtabs %}

**Q. What is the project url? (Optional)**

Optionally enter a link to your projects homepage. This info will go into the `plugin-details.yml` file and will be used to link to your project on Boost Protocol frontends.

**Q. What is the project icon url? (Optional)**

Optionally enter a url for the projects image. This logo will be shown on Boost Protocol frontends along with your boosts.

**Q. What is the action specific url**&#x20;

Optionally enter an action specific url. This is the webpage that you would like users to start their boost from. For example, if you are making a plugin for a swap action, you may want to link to https://myproject.xyz/swap

After answering all the questions the build process will begin. Once complete you will see your newly created project in the `packages/plugins` directory.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-03-09 at 15.52.48@2x (1).png" alt="" width="253"><figcaption><p>Our newly created project folder</p></figcaption></figure>

Once the builder is finished, please run the following commands:

{% code title="terminal" %}
```bash
pnpm install
pnpm build
pnpm format
```
{% endcode %}

Once your project is setup and built, you can start implementing the transaction filter in your newly created project folder, but first lets walkthrough some of the created files we will be interacting with.

* **src/\[Project].ts**: The main file where we will need to implement the logic for filtering transactions.
* **src/\[Project].test.ts**: The projects test file. This file brings in test cases from `test-transactions.ts`. No changes are required unless you want to add some custom testing logic.
* **src/test-transactions.ts**: This file contains the test cases that are used to test the logic and functionality of the plugin. If you provided a transaction hash and some transaction details in the CLI builder, there should be some test cases already generated for you, otherwise there will be a template you can use to make your own test cases. Please see the [Testing](../core-concepts/testing.md) page for more info on how to setup tests manually.
* **plugin-details.yml**: Contains metadata about your plugin. This metadata includes the projects url, and an icon that will be used for display purposes on frontends like Boost Inbox.
