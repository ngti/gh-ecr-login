# Login to Amazon ECR Action

Originates from [Push to Amazon ECR Action](https://github.com/jwalton/gh-ecr-push).

## Setup

To set this up, create a new IAM user with access to ECR (e.g. with the
AmazonEC2ContainerRegistryFullAccess policy).  Then, add the following secrets
to your GitHub project:

* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`

## Usage

```yaml
- name: Login to ECR
  id: ecr
  uses: ngti/gh-ecr-login@v1
  with:
    access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
    secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    region: eu-central-1
- name: Push to ECR
  env:
    REPOSITORY: my-image
    VERSION: v1
  run: |
    docker tag my-image ${{ steps.ecr.outputs.account }}.dkr.ecr.us-east-1.amazonaws.com/$REPOSITORY:$VERSION
    docker push ${{ steps.ecr.outputs.account }}.dkr.ecr.us-east-1.amazonaws.com/$REPOSITORY:$VERSION
```
