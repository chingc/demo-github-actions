# GitHub Actions

A collection of GitHub Actions workflows demonstrating various capabilities and features.

## basic.yml

<details>

<summary>A basic workflow to do the essentials.</summary>

<br/>If you're unfamiliar with GitHub Actions this will help you get started quickly.

[.github/workflows/basic.yml](.github/workflows/basic.yml)
- Runs when changes are pushed
- Runs on a schedule
- Can be run manually from the GitHub UI
- Uses [actions/checkout](https://github.com/actions/checkout)
- Uses [actions/setup-python](https://github.com/actions/setup-python) with pip cache
- Installs `requirements.txt` and runs a simple test
- Includes `dependabot.yml` to automatically check for package updates

</details>

## branch_name.yml

<details>

<summary>Getting the branch name.</summary>

<br/>This is a common CI operation. Surprisingly, there's no pre-defined way to get it in GitHub Actions.

This demo shows the simplest way without using 3rd party actions or other tools.

It works in most cases, but there are some quirks.

For example, if your commit is tagged this method will return the tag instead of the branch name. See SO link in the references for details.

You may also get an unexpected result depending on the event that triggered the workflow. This demo is set to trigger on `pull_request` and on `push` to illustrate this behavior.

[.github/workflows/branch_name.yml](.github/workflows/branch_name.yml)
- Shows various `github` context properties that may or may not contain the branch name
- Sets branch name to the top level `env` so it can be accessed by the entire workflow

</details>

## context.yml

<details>

<summary>Accessing information about workflow runs.</summary>

<br/>This can be helpful for debugging workflow errors or bugs, but be careful as it has the potential to output sensitive information.

[.github/workflows/context.yml](.github/workflows/context.yml)
- Shows various contexts

</details>

## env_var.yml

<details>

<summary>Working with environment variables.</summary>

<br/>Environment variables and their scopes work as you'd expect in GitHub Actions.

They're also fairly self-contained, so any changes you make are isolated to the job you're in.

One quirk that can cause confusion is the fact that environment variables defined within a step aren't accessible until the next step.

[.github/workflows/env_var.yml](.github/workflows/env_var.yml)
- Read env vars
- Write env vars
- Pass env vars

</details>

## github_script.yml

<details>

<summary>Using javascript in your workflow.</summary>

<br/>GitHub provides an action that lets you easily write javascript directly in your workflow.

The action also includes an object with the current workflow context, references to other useful packages, and it's a pre-authenticated octokit/rest.js client.

[.github/workflows/github_script.yml](.github/workflows/github_script.yml)
- Uses [actions/github-script](https://github.com/actions/github-script)

</details>

## homebrew.yml

<details>

<summary>Using homebrew in your workflow.</summary>

Leverage the convenience of homebrew to install applications on GitHub Actions runners.

[.github/workflows/homebrew.yml](.github/workflows/homebrew.yml)
- Uses [Homebrew/actions/setup-homebrew](https://github.com/Homebrew/actions/tree/master/setup-homebrew)

</details>

## system_path.yml

<details>

<summary>Working with the PATH environment variable.</summary>

<br/>Read, write, and modify PATH like any other environment variable.

[.github/workflows/system_path.yml](.github/workflows/system_path.yml)
- Modify PATH env var

</details>

## References

- [GitHub Docs: GitHub Actions](https://docs.github.com/en/actions)
<br/><br/>
- [GitHub Docs: Accessing contextual information about workflow runs](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/contexts)
- [GitHub Docs: Adding a system path](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions#adding-a-system-path)
- [GitHub Docs: Configuration options for the dependabot.yml file](https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file)
- [GitHub Docs: Events that trigger workflows](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows)
- [GitHub Docs: jobs.<job_id>.outputs](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions#jobsjob_idoutputs)
- [GitHub Docs: Setting an environment variable](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions#setting-an-environment-variable)
- [GitHub Docs: Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions)
<br/><br/>
- [octokit/rest.js API documentation](https://octokit.github.io/rest.js)
<br/><br/>
- [Stack Overflow: How to get a branch name on GitHub action when push on a tag?](https://stackoverflow.com/q/63745613)
- [Stack Overflow: How to get the current branch within Github Actions?](https://stackoverflow.com/q/58033366/808678)
