# Commands

{% hint style="info" %}
We use PNPM as the package manager for QuestDK-Plugins
{% endhint %}

To run commands on a specific package in your project, you can use the `--filter` option with various `pnpm` commands. This selective approach, detailed in [Turbo's filtering documentation](https://turbo.build/repo/docs/core-concepts/monorepos/filtering), optimizes efficiency, making it easier to manage individual parts of the project. The general structure of the command is:

<pre class="language-sh" data-title="terminal"><code class="lang-sh"><strong>
</strong><strong>pnpm &#x3C;command> --filter=@rabbitholegg/questdk-plugin-{project}
</strong><strong>
</strong></code></pre>

Replace `<command>` with the specific operation (like `test`, `lint`, etc.) and `{project}` with the name of your specific package.&#x20;

example: `pnpm test --filter@rabbitholegg/questdk-plugin-zora`

Here is a list of commands you will use for plugin development:

* `test`: Executes tests defined in the `src` folder of each package, typically named \[`Project].test.ts`.
* `build`: Runs the build process for your plugin, compiling code into a format ready for testing and deployment within the questDk-plugin ecosystem.
* `format`: Applies formatting rules from the Rome configuration file to the code files, ensuring consistency and readability in the project's coding style.
* `lint`: Analyzes the code for style issues and potential errors based on the Rome configuration file. Linting helps maintain code quality and standards.
* `changeset`: Used to generate a changeset, a record of changes in the codebase, which is useful for version tracking and understanding the evolution of the project. After running the command, follow the instructions in the terminal.

{% hint style="info" %}
For commands that should apply to the entire QuestDK-Plugins project, omit the `--filter` option. For example, to format all packages, simply use `pnpm format`.
{% endhint %}

{% content-ref url="helpful-tools.md" %}
[helpful-tools.md](helpful-tools.md)
{% endcontent-ref %}
