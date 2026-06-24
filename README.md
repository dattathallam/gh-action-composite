# Composite Greeter

A GitHub Actions composite action that demonstrates action composition: it checks out the repo, prints the runner OS, then delegates to [gh-action-node](https://github.com/dattathallam/gh-action-node) to produce a greeting message.

## Usage

```yaml
- uses: dattathallam/gh-action-composite@v1
  with:
    name: World
    greeting: Hello   # optional, defaults to "Hello"
```

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `name` | yes | — | Name to include in the greeting |
| `greeting` | no | `Hello` | Greeting word |

## Outputs

| Output | Description |
|--------|-------------|
| `message` | Full greeting message produced by the node action |

## Example

```yaml
jobs:
  greet:
    runs-on: ubuntu-latest
    steps:
      - uses: dattathallam/gh-action-composite@v1
        id: greet
        with:
          name: GitHub
          greeting: Hey

      - run: echo "${{ steps.greet.outputs.message }}"
```

## How it works

This is a **composite action** — it chains multiple steps (including other actions) into a single reusable unit:

1. `actions/checkout@v4` — checks out the calling repo
2. A `run` step that prints the runner OS
3. `dattathallam/gh-action-node@main` — produces the greeting output

Composite actions are defined entirely in `action.yml` with no compiled code.
