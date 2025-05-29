# update-pre-commit-action

[![OpenSSF Best Practices](https://www.bestpractices.dev/projects/10601/badge)](https://www.bestpractices.dev/projects/10601) [![CI](https://github.com/tagdots/update-pre-commit/actions/workflows/ci.yaml/badge.svg)](https://github.com/tagdots/update-pre-commit/actions/workflows/ci.yaml) [![Code Coverage](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/tagdots/update-pre-commit/refs/heads/badge/coverage.json)](https://github.com/tagdots/update-pre-commit/actions/workflows/cron-coverage.yaml)


This action uses [**update-pre-commit**](https://github.com/tagdots/update-pre-commit) to keep your `pre-commit` configuration up to date and

1. reduces your supply chain risks by following best practices in its development and operation.
1. simplifies your change management process by having both _updates_ and _pull request_ in the same code base.
1. protects you by not accepting revs tagged with "_alpha_", "_beta_", "_prerelease_", and "_rc_".

<br>

## 😎 Roll out 1 2 3

1. use the example workflows below to create your own workflow inside `.github/workflows`.
1. merge your code with the new workflow.
1. done!!

<br>

## 🔍 How to use update-pre-commit-action?

### Use Case 1️⃣ - example workflow
```
name: update-pre-commit-action

on:
  # on schedule: e.g. every day at 5:30 pm UTC
  schedule:
    - cron: '30 17 * * *'

  # on demand
  workflow_dispatch:

permissions:
  contents: read
  pull-requests: read

jobs:
  update-pre-commit:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: write

    steps:
    - name: Run update-pre-commit
      id: update-pre-commit
      env:
        GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      uses: tagdots/update-pre-commit-action@1.0.0
      with:
        file: .pre-commit-config.yaml
        dry-run: false
        open-pr: true
```

<br>

### Use Case 1️⃣ - summary descriptions
The above GitHub action workflow will:

* review the configuration file on a scheduled interval (`- cron: '30 17 * * *'`)
* need write permissions to contents and pull-requests (`contents: write` and `pull-requests: write`)
* update the configuration file - `.pre-commit-config.yaml` (`dry-run: false`)
* open a pull request when updates become available (`open-pr: true`)

<br>

### Use Case 2️⃣ - example workflow
```
name: update-pre-commit-action

on:
  # on schedule: e.g. every day at 5:30 pm UTC
  schedule:
    - cron: '30 17 * * *'

  # on demand
  workflow_dispatch:

permissions:
  contents: read
  pull-requests: read

jobs:
  update-pre-commit:
    runs-on: ubuntu-latest

    steps:
    - name: Run update-pre-commit
      id: update-pre-commit
      env:
        GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      uses: tagdots/update-pre-commit-action@1.0.0
      with:
        file: .pre-commit-config.yaml
        dry-run: false
        open-pr: false
```

<br>

### Use Case 2️⃣ - summary descriptions
The above GitHub action workflow will:

* review the configuration file on a scheduled interval (`- cron: '30 17 * * *'`)
* update the configuration file - `.pre-commit-config.yaml` (`dry-run: false`)
* _NOT_ open a pull request when updates become available (`open-pr: false`)

You will review the workflow results, cherry-pick updates, and open a pull-request yourself.

<br>

## 😕  Troubleshooting

We are here to help - open an [issue](https://github.com/tagdots-dev/upc-action-test/issues)
