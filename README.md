# GitHub Actions

A collection of small GitHub Actions workflows demonstrating various capabilities and features to get you started.

## basic.yml

<details>

<summary>A basic workflow to do the essentials for a Python project.</summary>

<br/>If you're unfamiliar with GitHub Actions this will help you get started quickly.

- Runs when changes are pushed
- Runs on a schedule
- Can be run manually from the GitHub UI
- Uses `actions/checkout`
- Uses `actions/setup-python` with pip cache
- Installs `requirements.txt` and runs a simple test
- Includes `dependabot.yml` to automatically check for package updates

See the [workflow](.github/workflows/basic.yml).

</details>

## basic_uv.yml

<details>

<summary>Same as basic.yml but uses the uv project manager.</summary>

<br/>

See the [workflow](.github/workflows/basic_uv.yml).

</details>

## branch_name.yml

<details>

<summary>Getting the branch name.</summary>

<br/>This is a common CI operation. Surprisingly, there's no pre-defined way to get it in GitHub Actions.

This demo shows the simplest way without using 3rd party actions or other tools.

It works in most cases, but there are some quirks.

For example, if your commit is tagged this method will return the tag instead of the branch name. See SO link in the references for details.

You may also get an unexpected result depending on the event that triggered the workflow. This demo is set to trigger on `pull_request` and on `push` to illustrate this behavior.

- Shows various `github` context properties that may or may not contain the branch name
- Sets branch name to the top level `env` so it can be accessed by the entire workflow

See the [workflow](.github/workflows/branch_name.yml).

</details>

## cache.yml

<details>

<summary>Caching data.</summary>

<br/>You can cache files, directories, or a combination of them. If you want to test for a cache hit, keep in mind that it only occurs if it matches the primary cache `key`. A partial match on `restore-keys` is still considered a cache miss.

- Uses `actions/cache`

See the [workflow](.github/workflows/cache.yml).

</details>

## context.yml

<details>

<summary>Accessing context information about workflow runs.</summary>

<br/>You can access various contexts about the workflow run, which can be helpful for debugging workflow errors or bugs. Be careful as it has the potential to output sensitive information.

See the [workflow](.github/workflows/context.yml).

</details>

## env_var_*.yml

<details>

<summary>Working with environment variables.</summary>

<br/>Environment variables and their scopes work as you'd expect in GitHub Actions.

They're also fairly self-contained, so any changes you make are isolated to the job you're in.

One quirk that can cause confusion is the fact that environment variables defined within a step aren't accessible until the next step.

See the workflows:
- [Reading](.github/workflows/env_var_read.yml)
- [Writing](.github/workflows/env_var_write.yml)
- [Passing](.github/workflows/env_var_pass.yml)
- [System PATH](.github/workflows/env_var_path.yml)

</details>

## github_script.yml

<details>

<summary>Scripting in workflows.</summary>

<br/>Easily and quickly write JavaScript in your workflow that uses the GitHub API and the workflow run context. The action includes a pre-authenticated octokit/rest.js client and references to many other useful packages.

- Uses `actions/github-script`

See the [workflow](.github/workflows/github_script.yml).

</details>

## homebrew.yml

<details>

<summary>Using homebrew in your workflow.</summary>

<br/>Leverage the convenience of homebrew to install applications on GitHub Actions runners.

- Uses `Homebrew/actions/setup-homebrew`

See the [workflow](.github/workflows/homebrew.yml).

</details>

## job_summary.yml

<details>

<summary>Custom output for the summary page of a workflow run.</summary>

<br/>You can set custom Markdown for each job so it will be displayed on the summary page of a workflow run. Job summaries support GitHub flavored Markdown, and you can add your Markdown content for a step to the `GITHUB_STEP_SUMMARY` environment file.

When a job finishes, the summaries for all steps in a job are grouped together into a single job summary and are shown on the workflow run summary page. If multiple jobs generate summaries, the job summaries are ordered by job completion time.

Job summaries are isolated between steps and each step is restricted to a maximum size of 1MB. A maximum of 20 job summaries from steps are displayed per job.

See the [workflow](.github/workflows/job_summary.yml).

</details>

## mise.yml

<details>

<summary>Using mise in your workflow.</summary>

<br/>The polyglot tool version manager.

- Uses `jdx/mise-action`

See the [workflow](.github/workflows/mise.yml).

</details>

## References

- [GitHub Actions](https://docs.github.com/en/actions)
- [GitHub Actions: Accessing contextual information about workflow runs](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/contexts)
- [GitHub Actions: Adding a job summary](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions#adding-a-job-summary)
- [GitHub Actions: Adding a system path](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions#adding-a-system-path)
- [GitHub Actions: Caching dependencies to speed up workflows](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/caching-dependencies-to-speed-up-workflows)
- [GitHub Actions: Events that trigger workflows](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows)
- [GitHub Actions: jobs.<job_id>.outputs](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions#jobsjob_idoutputs)
- [GitHub Actions: Setting an environment variable](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions#setting-an-environment-variable)
- [GitHub Actions: Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions)
<br/><br/>
- [actions/cache](https://github.com/actions/cache)
- [actions/checkout](https://github.com/actions/checkout)
- [actions/github-script](https://github.com/actions/github-script)
- [actions/setup-python](https://github.com/actions/setup-python)
- [Homebrew/actions/setup-homebrew](https://github.com/Homebrew/actions/tree/master/setup-homebrew)
- [jdx/mise-action](https://github.com/jdx/mise-action)
<br/><br/>
- [GitHub Docs: Dependabot options reference](https://docs.github.com/en/code-security/dependabot/working-with-dependabot/dependabot-options-reference)
<br/><br/>
- [octokit/rest.js API documentation](https://octokit.github.io/rest.js)
<br/><br/>
- [Stack Overflow: How to get a branch name on GitHub action when push on a tag?](https://stackoverflow.com/q/63745613)
- [Stack Overflow: How to get the current branch within Github Actions?](https://stackoverflow.com/q/58033366/808678)
