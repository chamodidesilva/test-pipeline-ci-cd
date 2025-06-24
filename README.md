## Authenticating github actions to aws

### identity federation using OIDC

resources 

https://aws.amazon.com/blogs/security/use-iam-roles-to-connect-github-actions-to-actions-in-aws/
https://docs.github.com/en/actions/security-for-github-actions/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services

this fix worked

https://github.com/aws-actions/configure-aws-credentials/issues/318

```sh
aws ecr create-repository \
--repository-name test-pipeline \
--region ap-south-1
```

```sh
aws iam create-role \
--role-name GitHubAction-AssumeRoleWithAction \
--assume-role-policy-document file://trustpolicyforGitHubOIDC.json
```

```sh
aws iam create-policy \
--policy-name my-get-identity-policy \
--policy-document file://policy.json
```

```sh
aws iam attach-role-policy \
--policy-arn arn:aws:iam::647264525674:policy/my-get-identity-policy \
--role-name GitHubAction-AssumeRoleWithAction
```