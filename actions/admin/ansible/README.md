# admin/ansible

Run an Ansible playbook located in `./shared/ansible` (typically checked out via [actions/_shared](../../_shared)).

This action is configured via workflow environment variables.

## Expectations

- Your workflow checks out this repo (so the action is available).
- Your workflow also checks out your shared library repo into `./shared` (so `shared/ansible/` exists).
- Inventory is either already present at `shared/ansible/inventory/hosts`, or provided as an artifact (see below).

## Configuration (env)

Required:

- `SSH_KEY` (required): SSH private key used to access hosts.

Optional:

- `ANSIBLE_PLAYBOOK_NAME` (optional): playbook file name (relative to `shared/ansible/`). Default: `playbook.yml`
- `ANSIBLE_EXTRA_ARGS` (optional): extra args passed to `ansible-playbook`.
- `ANSIBLE_LIMIT` (optional): `--limit` value. Default: `all` (also supports legacy `ENV`).

Inventory options:

- `ANSIBLE_INVENTORY_FILE` (optional): inventory file path. Default: `shared/ansible/inventory/hosts`
- `ANSIBLE_INVENTORY_ARTIFACT_NAME` (optional): artifact name to download if inventory file is missing. Default: `ansible-inventory-file`
- `ANSIBLE_INVENTORY_ARTIFACT_PATH` (optional): where to extract the artifact. Default: `shared/ansible/inventory`

Jump host options (optional):

- `ANSIBLE_JUMP_HOST` (optional): bastion/jump host address.
- `ANSIBLE_JUMP_PORT` (optional): preferred SSH port for jump host. Default: `22`
- `ANSIBLE_JUMP_USER` (optional): SSH username for jump host. Default: `SSH_USER` or `terraform`
- `SSH_USER` (optional): SSH username for target hosts. Default: `terraform`
- `SSH_PORT` (optional): SSH port for target hosts. Default: `22`

Collections update playbook:

- `ANSIBLE_COLLECTIONS_PLAYBOOK` (optional): playbook used to update/install collections. Default: `_update-ansible-collections.yml`

## Env-only example

```yaml
env:
  SHARED_REPO_NAME: BestianCode/devops-shared-library
  SHARED_REPO_BRANCH: main
  SHARED_FOLDER: ./shared

  SSH_KEY: ${{ secrets.SSH_KEY }}
  SSH_USER: terraform
  ANSIBLE_PLAYBOOK_NAME: playbook.yml
  ANSIBLE_LIMIT: all
  ANSIBLE_EXTRA_ARGS: "-vv"

steps:
  - uses: actions/checkout@v4
  - uses: BestianCode/github/actions/_shared@v1

  # If your inventory is produced earlier as an artifact, it will be downloaded automatically
  # when shared/ansible/inventory/hosts is missing.
  - uses: BestianCode/github/actions/admin/ansible@v1
```
