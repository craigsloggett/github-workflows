# github-workflows

A collection of reusable GitHub Actions workflows shared across my projects.

Reusable workflows let many repositories call a single, centrally maintained workflow instead of copying the same YAML into each one. Keeping them here means a fix made in one place rolls out everywhere that references it.

## Usage

Reference a workflow from another repository with `uses:`, pinned to a release tag or commit SHA:

```yaml
jobs:
  example:
    uses: craigsloggett/github-workflows/.github/workflows/<workflow>.yml@<ref>
```

## Update Terraform Provider Toolchain

`update-terraform-provider.yml` opens pull requests that bump pinned tool versions Dependabot cannot reach, such as `Makefile` variables and action inputs. Call it on a schedule from a Terraform provider repository:

```yaml
on:
  schedule:
    - cron: '0 8 * * 1'

jobs:
  update:
    uses: craigsloggett/github-workflows/.github/workflows/update-terraform-provider.yml@<ref>
    secrets:
      GH_TOKEN: ${{ secrets.UPDATE_TOKEN }}
```

It updates terraform, govulncheck, golangci-lint, and tfplugindocs by default; pass a `tools` input to change the set. `GH_TOKEN` must be a personal access token, not `github.token`, so the bump pull requests trigger workflows.
