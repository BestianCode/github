# aws/s3Sync

Sync a local folder to S3 (using `aws s3 sync --delete`) and optionally invalidate a CloudFront distribution matched by alias.

This action is configured via workflow environment variables (same style as [actions/_shared](../../_shared)).

## Configuration (env)

- `AWS_ACCESS_KEY_ID` (required)
- `AWS_SECRET_ACCESS_KEY` (required)
- `AWS_DEFAULT_REGION` (required)
- `BUCKET_NAME` (required): used as S3 bucket name (`s3://${BUCKET_NAME}`) and as CloudFront alias to find the distribution.

Optional:

- `SOURCE_FOLDER` (optional): local folder to sync. Default: `dist/`
- `DESTINATION_FOLDER` (optional): prefix inside the bucket (no leading/trailing `/` needed)
- `INVALIDATE_CLOUDFRONT` (optional): set to `false` to skip invalidation. Default: `true`
- `INVALIDATE_PATHS` (optional): paths passed to `aws cloudfront create-invalidation`. Default: `/*`

## Env-only example

```yaml
env:
  AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
  AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
  AWS_DEFAULT_REGION: eu-central-1
  BUCKET_NAME: example.com
  SOURCE_FOLDER: dist/
  DESTINATION_FOLDER: app
  INVALIDATE_PATHS: /index.html /assets/*

steps:
  - uses: actions/checkout@v4
  - uses: BestianCode/github/actions/aws/s3Sync@v1
```
