# Sync up to AWS CodeCommit Action

Synchronize from GitHub repository to AWS CodeCommit via GitHub Actions.  
No need to ssh-private-key. Need to AWS IAM Credentials only.

## Example usage

```yaml
name: Sync to AWS codecommit

on:
  push:
    tags-ignore:
      - '*'
    branches:
      - '*'

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION_ID }}

      - name: Sync up to CodeCommit
        uses: NaveenKumarThangamuthu/HikeOn_AWS_Code_Sync@v2.1
        with:
          repository_name: ${{ secrets.AWS_REPOSITORY_NAME }}
          aws_region:  ${{ secrets.AWS_REGION_ID }}
```

## Inputs

- `repository_name` **Required** CodeCommit repository name.
- `aws_region` **Required** Region of the CodeCommit repository.

## Author

[NaveenThangam](https://github.com/NaveenKumarThangamuthu/HikeOn_AWS_CodeCommit_Sync)
