[![StepSecurity Maintained Action](https://raw.githubusercontent.com/step-security/maintained-actions-assets/main/assets/maintained-action-banner.png)](https://docs.stepsecurity.io/actions/stepsecurity-maintained-actions)

# Craft Prepare Release Action

[![GitHub release](https://img.shields.io/github/release/step-security/getsentry-craft.svg)](https://github.com/step-security/getsentry-craft/releases/latest)
[![license](https://img.shields.io/github/license/step-security/getsentry-craft.svg)](https://github.com/step-security/getsentry-craft/blob/master/LICENSE)

GitHub Action that automates the `craft prepare` release workflow — creates a release branch, bumps the version, generates a changelog, and opens a publish request issue.

## Usage

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
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v7
        with:
          fetch-depth: 0
      - uses: step-security/getsentry-craft@v2
        with:
          version: ${{ github.event.inputs.version }}
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Inputs

| Input                            | Description                                                                      | Default                                       |
| -------------------------------- | -------------------------------------------------------------------------------- | --------------------------------------------- |
| `version`                        | Version to release (semver, `"auto"`, `"major"`, `"minor"`, `"patch"`)           | Uses `versioning.policy` from config          |
| `merge_target`                   | Target branch to merge into                                                      | Default branch                                |
| `force`                          | Force release even with blockers                                                 | `false`                                       |
| `blocker_label`                  | Label that blocks releases                                                       | `release-blocker`                             |
| `publish_repo`                   | Repository for publish issues. Use `"self"` to create issues in the source repo. | `{owner}/publish`                             |
| `git_user_name`                  | Git committer name                                                               | `github.actor`                                |
| `git_user_email`                 | Git committer email                                                              | `{actor_id}+{actor}@users.noreply.github.com` |
| `path`                           | Path that Craft will run inside                                                  | `.`                                           |
| `workspace`                      | Named Craft release workspace                                                    |                                               |
| `craft_config_from_merge_target` | Use craft config from the merge target branch                                    | `false`                                       |
| `craft_version`                  | Version of Craft to install                                                      | Action ref (e.g. `v2`)                        |

## Outputs

| Output           | Description                              |
| ---------------- | ---------------------------------------- |
| `version`        | The resolved version being released      |
| `branch`         | The release branch name                  |
| `sha`            | The commit SHA on the release branch     |
| `previous_tag`   | The tag before this release              |
| `changelog`      | The changelog for this release           |
| `changelog_file` | Path to the full changelog file          |
| `issue_url`      | URL of the created publish request issue |

## License

MIT
