# hoconfmt-action

Composite GitHub Action that formats changed `.conf` files on an internal pull
request and pushes the result back to the PR branch.

Behavior:

- Only runs when the PR creator invokes it
- Only writes back to internal PR branches
- Downloads a released `hoconfmt` binary instead of building from source

Minimal workflow usage:

```yaml
name: Format PR via Comment

on:
  issue_comment:
    types: [created]

permissions:
  contents: write
  pull-requests: read

jobs:
  format:
    if: github.event.issue.pull_request && github.event.comment.body == '/hoconfmt'
    runs-on: ubuntu-latest
    steps:
      - uses: lzm0/hoconfmt-action@main
        with:
          formatter-version: v0.1.2
```
