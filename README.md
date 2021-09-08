# remove-ansi-colors

[![License](https://img.shields.io/badge/license-MIT-blue)](http://opensource.org/licenses/mit-license.php) [![Issues](https://img.shields.io/github/issues/marcransome/remove-ansi-colors)](https://github.com/marcransome/remove-ansi-colors/issues)

A GitHub action for removing ANSI color escape sequences from arbitrary strings.

## Prerequisites

This action has a few dependencies that are generally satisfied by most [GitHub-hosted runners](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners) (`macos-*` and `ubuntu-*` environment variants):

* [GNU Bash](https://www.gnu.org/software/bash/)
* [Perl](https://www.perl.org)


## Usage

Add a suitable `uses` step to your GitHub [workflow](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions) with a value for the `colored` step input (i.e. a string that includes ANSI color escape sequences) and use the `uncolored` output in subsequent steps:

```yaml
jobs:
  remove-ansi-colors:
    runs-on: ubuntu-latest
    steps:
      - name: A step that generates output with ANSI color escape sequences
        id: generate-colored-output
        run: ...
      - name: Remove ANSI color codes
        uses: marcransome/remove-ansi-colors@main
        id: remove-ansi-colors
        with:
          colored: ${{ steps.generate-colored-output.outputs.stdout }}
      - name: Use uncolored output
        run: echo "${{ steps.remove-ansi-colors.outputs.uncolored }}"
```

## Action versions

Use one of the following patterns when specifying the version reference for this action in your workflow (i.e. the `{ref}` value in `uses: marcransome/remove-ansi-colors@{ref}`):

| Pattern  | Example   | Description                                                            |
|----------|-----------|------------------------------------------------------------------------|
| `vX`     | `v1`      | the latest `v1.*` release including non-breaking changes and bug fixes |
| `vX.Y`   | `v1.1`    | the latest `v1.1.*` release including bug fixes                        |
| `vX.Y.Z` | `v1.1.0`  | the `v1.1.0` release only                                              |

The recommended pattern is `vX` (e.g. `v1`). This will ensure that the version of the action used in your workflow includes the latest non-breaking changes and bug fixes, and guarantees compatibility with previous versions of that major release number.

Using a `main` branch reference in your workflow is _not_ recommended as this branch may include breaking changes intended for the next major release.


## License
`remove-ansi-colors` is provided under the terms of the [MIT License](http://opensource.org/licenses/mit-license.php).

## Contact
Email me at [marc.ransome@fidgetbox.co.uk](mailto:marc.ransome@fidgetbox.co.uk) or tweet [@marcransome](http://www.twitter.com/marcransome).
