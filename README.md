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
