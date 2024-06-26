---
description: How to contribute, the Pull Request process, and code style guidelines.
---

# Contribution Guidelines

### Commit Standards

Use [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/#summary) for commit messages, focusing on a single functionality per commit. This practice helps in creating a clear commit history and simplifies automated processes like changelog generation and semantic versioning. Keep your commits descriptive yet succinct.

### Style Guide

Our code style is governed by a specific Rome configuration, ensuring consistency and best practices across our codebase. Key formatting rules include:

* **Indentation:** 2 spaces
* **Line Width:** 80 characters
* **Semicolons:** as needed
* **Quotes:** single
* **Trailing commas:** Yes

The [`rome.json`](https://github.com/rabbitholegg/questdk-plugins/blob/main/rome.json) configuration file can be found in the root of the project if we want to see the full configuration.

Please format your code before submitting your Pull Request. You can format your code by running the command:

{% code title="terminal" %}
```bash
pnpm format
```
{% endcode %}

***

### Submitting a Pull Request

Please be as descriptive as possible when submitting your pull request. Include in the description:

* any implementation details that are relevant for the reviewers
* links to the projects documentation
* any limitations or irregularities that are present in the plugin

In order to publish your plugin you need to make sure that the pull request you're submitting has a changeset. In order to generate a changeset run `pnpm changeset`, select a change type \[major,minor,patch], and draft a small summary of the changeset. Select the version based on [semantic versioning](https://semver.org/).

Once you have submitted your Pull Request, it will be reviewed by the boost team. Once your Pull request has been approved, you will be able to see your project on [Boost Manager](https://manager.boost.xyz/registry). 🚀
