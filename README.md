[![StepSecurity Maintained Action](https://raw.githubusercontent.com/step-security/maintained-actions-assets/main/assets/maintained-action-banner.png)](https://docs.stepsecurity.io/actions/stepsecurity-maintained-actions)

# Craft Prepare Release Action

[![GitHub release](https://img.shields.io/github/release/step-security/getsentry-craft.svg)](https://github.com/step-security/getsentry-craft/releases/latest)
[![license](https://img.shields.io/github/license/step-security/getsentry-craft.svg)](https://github.com/step-security/getsentry-craft/blob/master/LICENSE)

GitHub Action that automates the `craft prepare` release workflow — creates a release branch, bumps the version, generates a changelog, and opens a publish request issue.

Craft is a command line tool that helps automate and pipeline package releases. It enforces a specific workflow for managing release branches, changelogs, and artifact publishing.

📚 **[Full Documentation](https://craft.sentry.dev/)**

## Quick Start

### Installation

```shell
curl -fsSL https://craft.sentry.dev/install | bash
```

Homebrew (`brew install getsentry/tools/craft`), standalone binaries, and npm
(`npm install -g @sentry/craft`) are also available. See
[Installation](https://craft.sentry.dev/installation/).

### Usage

```shell
# Auto-determine version from conventional commits
craft prepare auto

# Or specify a version explicitly
craft prepare 1.2.3

# Publish to all configured targets
craft publish 1.2.3
```

See the [Quick Start](https://craft.sentry.dev/getting-started/) to set up a project.

## Features

- **[Auto Versioning](https://craft.sentry.dev/versioning/)** - Determine version bumps from conventional commits, or use CalVer
- **[Multiple Targets](https://craft.sentry.dev/targets/)** - Publish to GitHub, npm, PyPI, Docker, crates.io, NuGet, and more
- **[Changelog Management](https://craft.sentry.dev/changelogs/)** - Auto-generate changelogs from pull requests or validate manual entries
- **[AI Changelog Summaries](https://craft.sentry.dev/ai-summaries/)** - Optional release, category, and scope summaries on top of generated changelogs
- **[Monorepo Support](https://craft.sentry.dev/workspaces/)** - Release independently versioned products from one repository with release workspaces
- **[CI Integration](https://craft.sentry.dev/release-workflow/)** - Wait for CI to pass, download artifacts, and publish
- **[GitHub Actions](https://craft.sentry.dev/github-actions/)** - Reusable workflows for releases and changelog previews

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
