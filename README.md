# Poetry Setup - GitHub Action

This GitHub Action installs a specified version of [Poetry](https://python-poetry.org/) using a specified version of Python. It supports caching the Poetry installation for faster workflows.

## Inputs

| Name            | Description                                         | Required | Default                                   |
|-----------------|-----------------------------------------------------|----------|-------------------------------------------|
| python-version  | Python version to use (e.g., `3.11`, `3.8`)         | true     | `3`                                       |
| poetry-version  | Poetry version to install (e.g., `1.7.1`)           | false    | (latest available)                        |
| poetry-home     | Directory where Poetry will be installed            | true     | `${{ github.workspace }}/.poetry`         |
| cache           | Enable Poetry installation caching (`true`/`false`) | false    | `true`                                    |

## Outputs

| Name           | Description                                         |
|----------------|-----------------------------------------------------|
| python-path    | The path to the Python executable                   |
| python-version | The version of Python that was installed            |
| poetry-setup   | The version of Poetry that was installed            |
| poetry-home    | The home directory where Poetry was installed       |

## Example Usage

```yaml
jobs:
  my-job:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: miklinux/poetry-setup@main
        id: poetry
        with:
          python-version: '3.11'
          poetry-setup: '1.7.1'
          poetry-home: '${{ github.workspace }}/.poetry'
          cache: true

      - name: Show Poetry version
        run: poetry --version


