# Demo

A collection of GitHub Actions workflows where I demonstrate various capabilities and features.

They serve as a quickstart and reference for my future self. Each are described below.

## basic.yml

The most basic workflow to do all the essentials.

- Runs when changes are pushed
- Runs on a schedule
- Can be run manually from the GitHub UI
- Uses [actions/checkout](https://github.com/actions/checkout)
- Uses [actions/setup-python](https://github.com/actions/setup-python) with pip cache
- Installs `requirements.txt` and runs a simple test
- Includes `dependabot.yml` to automatically check for package updates

## context.yml

Contexts are a way to access information about workflow runs, variables, runner environments, jobs, and steps.

This can be helpful for debugging workflow errors or bugs.

> Warning: Be careful when printing the entire context as it may contain sensitive information.

- Shows various contexts

## github_script.yml

GitHub provides an action that lets you easily write javascript directly in your workflow.

The action includes an object with the current workflow context and references to several other useful packages. It's also a pre-authenticated octokit/rest.js client.

- Uses [actions/github-script](https://github.com/actions/github-script)

## References

- [GitHub Docs: GitHub Actions](https://docs.github.com/en/actions)
- [GitHub Docs: Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions)
- [GitHub Docs: Configuration options for the dependabot.yml file](https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file)
- [GitHub Docs: Accessing contextual information about workflow runs](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/contexts)
- [octokit/rest.js API documentation](https://octokit.github.io/rest.js)
