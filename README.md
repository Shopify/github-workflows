# github-workflows

GitHub reusable workflows for public Shopify repositories. Not specific to any implementation/ecosystem.

## Using a workflow

We suggest you reference workflows by their git commit.
If you include a commit and tag on the same line, Dependabot will maintain both references. Example: `uses: Shopify/github-workflows/.github/workflows/scorecard.yaml@0cd53e568340d24a2aefc65236f0973b47402c14 # v0.0.1`

<details>
<summary>Dependabot Configuration</summary>

Create/modify the `.github/dependabot.yaml` file in your repository. Make sure the `updates` block contains a `github-actions` entry.

```yaml
version: 2
updates:
- package-ecosystem: github-actions
  directory: /
  schedule:
    interval: weekly
```
  
</details>

## Available workflows

### scorecard.yaml

Publish an [OpenSSF Scorecard](https://securityscorecards.dev/) for a project.
Use this in public repositories, so that consumers can be assured of Shopify's security practices.

Consider adding a badge like `https://api.securityscorecards.dev/projects/github.com/Shopify/github-workflows/badge`.

<details>
<summary>Example Workflow</summary>
  
```yaml
name: Scorecard
on:
  branch_protection_rule:
  schedule:
    - cron: '30 1 * * 6'

permissions: {}

jobs:
  build:
    permissions:
      contents: read
      id-token: write
    uses: Shopify/github-workflows/.github/workflows/scorecard.yaml@0cd53e568340d24a2aefc65236f0973b47402c14 # v0.0.1
    secrets:
      token: ${{secrets.GITHUB_TOKEN}}
```
</details>

