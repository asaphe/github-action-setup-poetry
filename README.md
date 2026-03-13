# github-action-setup-poetry

A composite GitHub Action that installs Poetry, sets up Python, manages dependencies with caching, and reports cache performance.

## Usage

```yaml
- uses: asaphe/github-action-setup-poetry@v1
  with:
    python-version: "3.12.8"
    working-directory: "python"
    dependency-groups: "--with dev"
```

### With Custom Cache Key

```yaml
- uses: asaphe/github-action-setup-poetry@v1
  with:
    working-directory: "backend"
    cache-key-suffix: "-lint"
```

## Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `version` | Poetry version to install | No | `2.0.1` |
| `working-directory` | Working directory for poetry commands | No | `python` |
| `dependency-groups` | Poetry dependency groups to install | No | `--with dev` |
| `python-version` | Python version to use | No | `3.12.8` |
| `setup-pipx` | Whether to setup pipx (for self-hosted runners) | No | `false` |
| `cache-key-suffix` | Additional suffix for cache key (for parallel jobs) | No | `""` |

## Outputs

| Name | Description |
|------|-------------|
| `cache-hit` | Whether the poetry cache was hit |
| `poetry-version` | Installed Poetry version |

## What It Does

1. Sets up Python with pip caching
2. Optionally installs pipx (for self-hosted runners)
3. Installs Poetry via `snok/install-poetry`
4. Configures in-project virtualenvs
5. Restores virtualenv from cache (keyed on `poetry.lock`)
6. Installs dependencies
7. Saves cache on miss
8. Reports cache performance

## License

Apache 2.0 - See [LICENSE](LICENSE) for details.
