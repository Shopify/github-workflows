# github-workflows

GitHub reusable workflows for common Shopify tasks.

### scorecard.yaml

Publish an [OpenSSF Scorecard](https://securityscorecards.dev/) for a project.
Use this in public repositories, so that consumers can be assured of Shopify's security practices.

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
    uses: Shopify/github-workflows/.github/workflows/scorecard.yaml@v1.0.0
    secrets:
      token: ${{secrets.GITHUB_TOKEN}}
```
</details>
