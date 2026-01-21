# _pull

Checkout a GitHub repository into a subfolder (useful for pulling shared libraries/modules into the workspace).

## Inputs

- `SHARED_REPO_NAME` (optional): `OWNER/REPO` to checkout. If omitted, falls back to `env.SHARED_REPO_NAME`.
- `SHARED_REPO_BRANCH` (optional): branch/tag/SHA to checkout. If omitted, falls back to `env.SHARED_REPO_BRANCH`. If still empty, the repo default branch is used.
- `GITHUB_TOKEN` (optional): token used by `actions/checkout`. Defaults to `${{ github.token }}`.
- `SHARED_FOLDER` (optional): target folder. Default: `./shared`.

## Example

```yaml
- name: Pull shared repo
  uses: BestianCode/github/actions/_pull@v1
  with:
    SHARED_REPO_NAME: BestianCode/devops-shared-library
    SHARED_REPO_BRANCH: main
    SHARED_FOLDER: ./shared
```

You can also provide `SHARED_REPO_NAME` / `SHARED_REPO_BRANCH` via `env:` if you prefer.
