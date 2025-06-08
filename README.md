# GitHub Actions

A collection of small GitHub Actions workflows demonstrating various capabilities and features to get you started.

## 1st Party

These examples use only tools and actions from GitHub.

### basic.yml

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

See the [workflow](.github/workflows/basic.yml) and [dependabot](.github/dependabot.yml).

</details>

### branch_name.yml

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

### cache.yml

<details>

<summary>Data persistence by caching.</summary>

<br/>You can cache files, directories, or a combination of them. If you want to test for a cache hit, keep in mind that it only occurs if it matches the primary cache `key`. A partial match on `restore-keys` is still considered a cache miss.

- Uses `actions/cache`

See the [workflow](.github/workflows/cache.yml).

</details>

### context.yml

<details>

<summary>Accessing context information about workflow runs.</summary>

<br/>You can access various contexts about the workflow run, which can be helpful for debugging workflow errors or bugs. Be careful as it has the potential to output sensitive information.

See the [workflow](.github/workflows/context.yml).

</details>

### env_var_*.yml

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

### github_script.yml

<details>

<summary>Scripting in workflows.</summary>

<br/>Easily and quickly write JavaScript in your workflow that uses the GitHub API and the workflow run context. The action includes a pre-authenticated octokit/rest.js client and references to many other useful packages.

- Uses `actions/github-script`

See the [workflow](.github/workflows/github_script.yml).

</details>

### job_summary.yml

<details>

<summary>Custom output for the summary page of a workflow run.</summary>

<br/>You can set custom Markdown for each job so it will be displayed on the summary page of a workflow run. Job summaries support GitHub flavored Markdown, and you can add your Markdown content for a step to the `GITHUB_STEP_SUMMARY` environment file.

When a job finishes, the summaries for all steps in a job are grouped together into a single job summary and are shown on the workflow run summary page. If multiple jobs generate summaries, the job summaries are ordered by job completion time.

Job summaries are isolated between steps and each step is restricted to a maximum size of 1MB. A maximum of 20 job summaries from steps are displayed per job.

See the [workflow](.github/workflows/job_summary.yml).

</details>

### log_annotation.yml

<details>

<summary>Create annotations in workflow logs.</summary>

<br/>You can create `notice`, `warning`, and `error` annotations in your workflow logs. Optionally, they can be associated with a file and even a position within the file. Annotations also show up on the job summary page.

See the [workflow](.github/workflows/log_annotation.yml).

</details>

### matrix.yml

<details>

<summary>Define a matrix of different job configurations.</summary>

<br/>The matrix strategy helps you easily target multiple operating systems and language versions.

- Uses `actions/setup-node`

See the [workflow](.github/workflows/matrix.yml).

</details>

### parallel_*.yml

<details>

<summary>Parallel testing without any code changes or extra dependencies.</summary>

<br/>The matrix strategy can be used in a particular way to enable parallel testing for free. "Free" meaning no code changes and no extra dependencies. This example uses Python, but can be adapted to any language. The idea is to identify where your tests are and distrubute them across multiple GitHub Actions runners. If your testing framework supports parallel testing, you can use it together with this strategy to really go fast!

Note: This will increase the number of runners used, so keep an eye on your usage to avoid billing surprises.

See the workflows:
- [Directory-level parallel testing](.github/workflows/parallel_dir.yml)
- [File-level parallel testing](.github/workflows/parallel_file.yml)

</details>

### workflow_input.yml

<details>

<summary>Adjust how a workflow will run with custom input.</summary>

<br/>When using the `workflow_dispatch` event, you can optionally specify inputs that are passed to the workflow.

This trigger only receives events when the workflow file is on the default branch. This means you have to merge your changes to `main` or `master` before you can test your inputs. It would be wise to try input changes in a totally separate workflow before merging them into critical workflows.

Also, if the event that triggers the workflow isn't `workflow_dispatch` the input values are empty/null. This is true even if you have default values defined.

See the [workflow](.github/workflows/workflow_input.yml).

</details>

## 3rd Party

These examples include tools and actions from 3rd parties.

### homebrew.yml

<details>

<summary>Using homebrew in your workflow.</summary>

<br/>Leverage the convenience of homebrew to install applications on GitHub Actions runners.

- Uses `Homebrew/actions/setup-homebrew`

See the [workflow](.github/workflows/homebrew.yml).

</details>

### mise.yml

<details>

<summary>Using mise in your workflow.</summary>

<br/>The polyglot tool and project manager.

- Uses `jdx/mise-action`

See the [workflow](.github/workflows/mise.yml).

</details>

### uv.yml

<details>

<summary>Using uv in your workflow.</summary>

<br/>Same as basic.yml but uses the uv Python project manager.

- Uses `astral-sh/setup-uv`

See the [workflow](.github/workflows/uv.yml).

</details>

## References

- [GitHub Actions](https://docs.github.com/en/actions)
- [GitHub Actions: Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions)
<br/><br/>
- [GitHub Actions: Accessing contextual information about workflow runs](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/contexts)
- [GitHub Actions: Adding a job summary](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions#adding-a-job-summary)
- [GitHub Actions: Adding a log annotation](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions#setting-a-notice-message)
- [GitHub Actions: Adding a system path](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions#adding-a-system-path)
- [GitHub Actions: Caching dependencies to speed up workflows](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/caching-dependencies-to-speed-up-workflows)
- [GitHub Actions: Evaluate expressions in workflows and actions](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/evaluate-expressions-in-workflows-and-actions)
- [GitHub Actions: Events that trigger workflows](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows)
- [GitHub Actions: Running variations of jobs in a workflow](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/running-variations-of-jobs-in-a-workflow)
- [GitHub Actions: Setting an environment variable](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions#setting-an-environment-variable)
<br/><br/>
- [actions/cache](https://github.com/actions/cache)
- [actions/checkout](https://github.com/actions/checkout)
- [actions/github-script](https://github.com/actions/github-script)
- [actions/setup-node](https://github.com/actions/setup-node)
- [actions/setup-python](https://github.com/actions/setup-python)
- [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv)
- [Homebrew/actions/setup-homebrew](https://github.com/Homebrew/actions/tree/master/setup-homebrew)
- [jdx/mise-action](https://github.com/jdx/mise-action)
<br/><br/>
- [GitHub Docs: Dependabot options reference](https://docs.github.com/en/code-security/dependabot/working-with-dependabot/dependabot-options-reference)
<br/><br/>
- [octokit/rest.js API documentation](https://octokit.github.io/rest.js)
<br/><br/>
- [Stack Overflow: How to get a branch name on GitHub action when push on a tag?](https://stackoverflow.com/q/63745613)
- [Stack Overflow: How to get the current branch within Github Actions?](https://stackoverflow.com/q/58033366/808678)
