# action-golang-gosum

Check if the go.mod and go.sum match the source code by running `go mod tidy` and send a Pull Request :rocket:

## Installation

Create a workflow yaml file (eg: `.github/workflows/go-mod-tidy.yml` see [Creating a Workflow file](https://help.github.com/en/articles/configuring-a-workflow#creating-a-workflow-file))

```yaml
name: 'go-mod-tidy'

on:
  push:
    branches:
      - 'master'
    paths:
      - 'go.mod'
      - 'go.sum'

jobs:
  fix:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-go@v2
        with:
          go-version: 1.14

      - name: tidy
        uses: paulvollmer/action-golang-gosum@v1.0.0
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Environment Variables

### `GITHUB_TOKEN`
**Required** to send the pull request.

### `COMMIT_MESSAGE`
Overwrite the default git commit message.

### `PR_BRANCH`
Overwrite the default git branch to write the git commit to.

### `PR_TITLE`
Overwrite the default pull request title.

### `PR_MESSAGE`
Overwrite the default pull request message.

### `PR_BASE`
Overwrite the default pull request base branch. Default is the `master` branch.

### `LET_FAIL`
Set to `yes` to not send a pull request and exit with `1`
