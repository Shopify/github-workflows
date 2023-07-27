# github-workflows

GitHub reusable workflows for public Shopify repositories. Not specific to any language or ecosystem.

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

<!-- Please keep this alphabetical and consistent <3 -->

### cla.yaml

Ensure any code contributors have signed the [Shopify CLA](https://cla.shopify.com).

<details>
<summary>Example Workflow</summary>

```yaml
name: Contributor License Agreement (CLA)

on:
  pull_request_target:
    types: [opened, synchronize]
  issue_comment:
    types: [created]

permissions: {}

jobs:
  cla:
    uses: Shopify/github-workflows/.github/workflows/cla.yaml@c142f2dd84228c90bd716e4b5eafc68bd812f467 # v0.0.3
    permissions:
      pull-requests: write
    secrets:
      token: ${{secrets.GITHUB_TOKEN}}
      cla-token: ${{secrets.CLA_TOKEN}}
```

</details>


### dependabot-automerge.yaml

Automatically approve and merge Dependabot PRs matching certain criteria. Supports filtering by ecosystem and semver gap, such as "all actions minor+patch updates".

Repositories using this workflow must:
* Have `Allow auto-merge` [enabled](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/automatically-merging-a-pull-request#enabling-auto-merge).
* Have branch protection enabled, with the `Require status checks to pass before merging` option enforcing CI.


<details>
<summary>Example Workflow</summary>

```yaml
name: Dependabot auto-merge
on:
  pull_request:
    types:
      - opened
      - reopened
      - synchronize
    paths:
      - '.github/workflows/**'

permissions: {}

jobs:
  automerge:
    permissions:
      contents: write
      pull-requests: write
    uses: Shopify/github-workflows/.github/workflows/dependabot-automerge.yaml@c395c2cfd65be9a36f5dcfd21f4a2498a477fed4 # v0.0.6
    with:
      actions: minor
```

</details>


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
    - cron: "30 1 * * 6"

permissions: {}

jobs:
  analysis:
    permissions:
      contents: read
      id-token: write
    uses: Shopify/github-workflows/.github/workflows/scorecard.yaml@0cd53e568340d24a2aefc65236f0973b47402c14 # v0.0.1
    secrets:
      token: ${{secrets.GITHUB_TOKEN}}
```

</details>
