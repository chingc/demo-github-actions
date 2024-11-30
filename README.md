# Demo

A collection of GitHub Actions workflows where I demonstrate various capabilities and features.

Each are described below. They serve as a quickstart and reference for my future self.

## basic.yml

The most basic workflow to do all the essentials.

- Runs when changes are pushed
- Runs on a schedule
- Can be run manually from the GitHub UI
- Uses [actions/checkout](https://github.com/actions/checkout)
- Uses [actions/setup-python](https://github.com/actions/setup-python) with pip cache
- Installs `requirements.txt` and runs a simple test
- Includes `dependabot.yml` to automatically check for package updates

## References

- [GitHub Docs: GitHub Actions](https://docs.github.com/en/actions)
- [GitHub Docs: Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions)
- [GitHub Docs: Configuration options for the dependabot.yml file](https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file)
