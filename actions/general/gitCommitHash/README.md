# general/gitCommitHash

Export a short git commit hash into the workflow environment via `$GITHUB_ENV`.

This action is configured via workflow environment variables (same style as [actions/_shared](../../_shared)).

## Configuration (env)

Optional:

- `COMMIT_HASH_LENGTH` (optional): length for `git rev-parse --short`. Default: `7`
- `GIT_COMMIT_ENV` (optional): env var name to set for the commit hash. Default: `GIT_COMMIT`
- `SET_K8S_COMMIT_HASH` (optional): set to `false` to skip the second variable. Default: `true`
- `K8S_COMMIT_HASH_ENV` (optional): env var name to set (when `SET_K8S_COMMIT_HASH=true`). Default: `K8S_COMMIT_HASH`

## Env-only example

```yaml
env:
  COMMIT_HASH_LENGTH: 7
  GIT_COMMIT_ENV: GIT_COMMIT
  SET_K8S_COMMIT_HASH: true
  K8S_COMMIT_HASH_ENV: K8S_COMMIT_HASH

steps:
  - uses: actions/checkout@v4
  - uses: BestianCode/github/actions/general/gitCommitHash@v1

  - name: Show hashes
    shell: bash
    run: |
      echo "GIT_COMMIT=${GIT_COMMIT}"
      echo "K8S_COMMIT_HASH=${K8S_COMMIT_HASH}"
```
