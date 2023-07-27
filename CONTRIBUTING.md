# Development

### I want to add a workflow

Please open an issue for discussion.
It's probably welcome, but our release model of tags and Dependabot discourages workflows that will update frequently.

### I want to change a workflow

PRs welcome!

Once the code has been pushed to a branch in this repository, you can modify your repository to test your feature branch. Example: `uses: Shopify/github-workflows/.github/workflows/scorecard.yaml@my-cool-branch`.

Testing branches does not require a PR, but feel free to open a draft and `@mention` if you'd like feedback.
Ideally PRs will be able to link to at least one example of their modifications running.

# Releasing

Use the GitHub UI at https://github.com/Shopify/github-workflows/releases/new to create a new release.

1. Create a tag that follows semantic versioning:
    * If you expect users will need to change their calling workflow, e.g. to provide new inputs, increment the major version and **be sure to note the breaking change in the release notes**.
    * If you're adding a new workflow, or a new feature that users must opt-in to, increment the minor version.
    * If you fixed a bug or made a transparent change, increment the patch version.
2. Leave the release title blank. If you really want to get creative, please be sure to include the version number.
3. Use the automatically generated changelog as a starter, but add any additional details.
