# GitHub Actions

This repository contains reusable GitHub Actions.

## Actions

- [actions/_shared](actions/_shared)
	- Checkout a GitHub repository into a folder.

- [actions/aws/s3Sync](actions/aws/s3Sync)
	- Sync a folder to S3 and optionally invalidate CloudFront.

- [actions/general/gitCommitHash](actions/general/gitCommitHash)
	- Export short git commit hash to GITHUB_ENV.

- [actions/admin/ansible](actions/admin/ansible)
	- Run an Ansible playbook from ./shared/ansible (optionally via jump host).
