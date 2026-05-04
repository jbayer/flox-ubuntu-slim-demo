# Flox on Ubuntu Slim Runner

Minimal example validating that [Flox](https://flox.dev) installs and `flox activate` works correctly on GitHub Actions `ubuntu-slim` runners.

## Background

The `ubuntu-slim` runner image has fewer pre-installed packages than `ubuntu-latest`, which can surface issues with the Nix daemon startup and Flox environment activation that don't appear on standard runners. This repo serves as a simple smoke test.

## What it tests

The [workflow](.github/workflows/test-flox-activate.yml) runs on both `ubuntu-slim` and `ubuntu-latest` and validates:

1. Flox installs successfully via [`flox/install-flox-action`](https://github.com/flox/install-flox-action)
2. `flox init` creates an environment
3. `flox install hello` adds a package
4. `flox activate -- hello` runs a command inside the activated environment
5. `flox activate` correctly sets up the shell (e.g. `which hello` resolves)

## Running locally

```bash
gh workflow run test-flox-activate.yml
```
