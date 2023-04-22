<img alt="paint" src="images/paint-roller.png" width="180" align="right">

# remove-ansi-colors

[![Tests](https://img.shields.io/github/actions/workflow/status/marcransome/remove-ansi-colors/test.yml?branch=main&color=brightgreen&label=tests)](https://github.com/marcransome/remove-ansi-colors/actions) [![Issues](https://img.shields.io/github/issues/marcransome/remove-ansi-colors)](https://github.com/marcransome/remove-ansi-colors/issues/) [![Dependabot](https://img.shields.io/badge/dependabot-active-brightgreen.svg)](https://github.com/marcransome/remove-ansi-colors/network/dependencies) [![License](https://img.shields.io/badge/license-MIT-blue)](https://opensource.org/licenses/mit-license.php)

A GitHub action for removing ANSI color escape sequences from arbitrary strings.

## Prerequisites

This action has a few dependencies that are generally satisfied by most [GitHub-hosted runners](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners) (`macos-*` and `ubuntu-*` environment variants):

* [GNU Bash](https://www.gnu.org/software/bash/)
* [Perl](https://www.perl.org)

## Usage

Add a suitable `uses` step to your GitHub [workflow](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions) with a value for the `colored` step input (i.e. an output from a previous step that includes ANSI color escape sequences) and use the `uncolored` output in subsequent steps:

```yaml
jobs:
  remove-ansi-colors:
    runs-on: ubuntu-latest
    steps:
      - name: A step that generates output with ANSI color escape sequences
        id: generate-colored-output
        run: |
          colored=$(printf '\e[0;31mCOLORED\e[0m')
          echo "{colored}={$colored}" >> "$GITHUB_OUTPUT"
      - name: Remove ANSI color escape sequences
        uses: marcransome/remove-ansi-colors@v1
        id: remove-ansi-colors
        with:
          colored: ${{ steps.generate-colored-output.outputs.colored }}
      - name: Use uncolored output
        run: echo "${{ steps.remove-ansi-colors.outputs.uncolored }}"
```

## Inputs

* `colored` - A string containing ANSI color escape sequences.

## Outputs

* `uncolored` - The `colored` input string with ANSI color escape sequences removed.

## Action versions

Use one of the following patterns when specifying the version reference for this action in your workflow (i.e. the `{ref}` value in `uses: marcransome/remove-ansi-colors@{ref}`):

| Pattern  | Example   | Description                                                            |
|----------|-----------|------------------------------------------------------------------------|
| `vX`     | `v1`      | the latest `v1.*` release including non-breaking changes and bug fixes |
| `vX.Y`   | `v1.1`    | the latest `v1.1.*` release including bug fixes                        |
| `vX.Y.Z` | `v1.1.0`  | the `v1.1.0` release only                                              |

The recommended pattern is `vX` (e.g. `v1`). This will ensure that the version of the action used in your workflow includes the latest non-breaking changes and bug fixes, and guarantees compatibility with previous versions of that major release number.

Using a `main` branch reference in your workflow is _not_ recommended as this branch may include breaking changes intended for the next major release.

## Acknowledgements

* Paint roller icon made by [Freepik](https://www.flaticon.com/authors/freepik) from [www.flaticon.com](https://www.flaticon.com/)

## License
`remove-ansi-colors` is provided under the terms of the [MIT License](https://opensource.org/licenses/mit-license.php).

## Contact
Email me at [marc.ransome@fidgetbox.co.uk](mailto:marc.ransome@fidgetbox.co.uk) or [create an issue](https://github.com/marcransome/remove-ansi-colors/issues).
