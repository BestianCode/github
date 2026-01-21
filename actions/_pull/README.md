# _pull

Checkout a GitHub repository into a subfolder (useful for pulling shared libraries/modules into the workspace).

## Configuration (env)

This action is configured via workflow environment variables:

- `SHARED_REPO_NAME` (required): `OWNER/REPO` to checkout.
- `SHARED_REPO_BRANCH` (optional): branch/tag/SHA to checkout. If omitted, the repo default branch is used.
- `SHARED_FOLDER` (optional): target folder. Default: `./shared`.
- `GITHUB_TOKEN` (optional): token used by `actions/checkout`. If omitted, `${{ github.token }}` is used.

## Env-only example

```yaml
env:
  SHARED_REPO_NAME: BestianCode/devops-shared-library
  SHARED_REPO_BRANCH: main
  SHARED_FOLDER: ./shared
  GITHUB_TOKEN: ${{ secrets.READ_GITHUB_TOKEN }}

steps:
  - uses: actions/checkout@v4
  - uses: BestianCode/github/actions/_pull@v1
```
