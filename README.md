# GitHub Actions

A collection of GitHub Actions workflows demonstrating various capabilities and features.

They serve as a quickstart and reference for my future self. Each are described below.

## basic.yml

A basic workflow to do all the essentials.

- Runs when changes are pushed
- Runs on a schedule
- Can be run manually from the GitHub UI
- Uses [actions/checkout](https://github.com/actions/checkout)
- Uses [actions/setup-python](https://github.com/actions/setup-python) with pip cache
- Installs `requirements.txt` and runs a simple test
- Includes `dependabot.yml` to automatically check for package updates

## branch_name.yml

Getting the branch name is a common CI operation. Surprisingly, there's no pre-defined way to get it in GitHub Actions.

This demo shows the simplest way without using 3rd party actions or invoking various tools.

It works in most cases, but there are some quirks.

For example, if your commit is tagged this method will return the tag instead of the branch name. See SO link in the references for details.

You may also get an unexpected result depending on the event that triggered the workflow. This demo is set to trigger on `pull_request` and on `push` to illustrate this behavior.

- Shows various `github` context properties that may or may not contain the branch name
- Sets branch name to the top level `env` so it can be accessed by the entire workflow

## context.yml

Contexts are a way to access information about workflow runs, variables, runner environments, jobs, and steps.

This can be helpful for debugging workflow errors or bugs.

> Warning: Be careful when printing the entire context as it may contain sensitive information.

- Shows various contexts

## env_var.yml

Environment variables and their scopes work as you'd expect in GitHub Actions.

They're also fairly self-contained, so any changes you make are isolated to the job you're in.

One quirk that can cause confusion is the fact that environment variables defined within a step aren't accessible until the next step.

- Read env vars
- Write env vars
- Pass env vars

## env_var_path.yml

Read, write, and modify PATH like any other environment variable. It has the same quirks.

- Modify PATH env var

## github_script.yml

GitHub provides an action that lets you easily write javascript directly in your workflow.

The action includes an object with the current workflow context and references to several other useful packages. It's also a pre-authenticated octokit/rest.js client.

- Uses [actions/github-script](https://github.com/actions/github-script)

## homebrew.yml

If you develop on macOS you're probably familiar with [homebrew](https://brew.sh).

Did you know it's also available on Linux?

This demo shows how you can leverage its power and convenience to install applications on GitHub Actions runners.

- Uses [Homebrew/actions/setup-homebrew](https://github.com/Homebrew/actions/tree/master/setup-homebrew)

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
