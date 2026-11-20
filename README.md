[![StepSecurity Maintained Action](https://raw.githubusercontent.com/step-security/maintained-actions-assets/main/assets/maintained-action-banner.png)](https://docs.stepsecurity.io/actions/stepsecurity-maintained-actions)

# Craft Prepare Release Action

[![GitHub release](https://img.shields.io/github/release/step-security/getsentry-craft.svg)](https://github.com/step-security/getsentry-craft/releases/latest)
[![license](https://img.shields.io/github/license/step-security/getsentry-craft.svg)](https://github.com/step-security/getsentry-craft/blob/master/LICENSE)

GitHub Action that automates the `craft prepare` release workflow — creates a release branch, bumps the version, generates a changelog, and opens a publish request issue.

Craft is a command line tool that helps automate and pipeline package releases. It enforces a specific workflow for managing release branches, changelogs, and artifact publishing.

## Configuration

Create a `.craft.yml` in your project root:

```yaml
minVersion: '2.21.0'
changelog:
  policy: auto
targets:
  - name: github
  - name: npm
    access: public
```

See the [configuration reference](https://craft.sentry.dev/configuration/) for all options.

## GitHub Actions

```yaml
name: Release
on:
  workflow_dispatch:
    inputs:
      version:
        description: 'Version to release (or "auto")'
        required: false

jobs:
  release:
    permissions:
      contents: write
    uses: step-security/getsentry-craft@v3
    with:
      version: ${{ inputs.version }}
    secrets: inherit
```

See [GitHub Actions](https://craft.sentry.dev/github-actions/) for all inputs,
the composite action, and the changelog preview workflow.

## License

MIT
