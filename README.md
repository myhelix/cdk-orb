# Terraform Orb

A CircleCI orb for custom terraform operations based on Helix requirements.

## Features

### Plan Comment

The Terraform Orb provides functionality to automatically post terraform plan outputs as GitHub PR comments. This feature makes it easier for team members to review Terraform changes directly within pull requests without needing to access CircleCI logs.

Key capabilities include:

- Automatic execution of `terraform plan` and posting its output as a GitHub PR comment
- AWS IAM role assumption via OIDC for secure access to AWS resources
- Verification that terraform plan has been run before posting the comment
- Flexible configuration for AWS region and secret name
- Option to use either AWS Secrets Manager or environment variables for GitHub tokens

## Usage

### Plan Comment

To use the Plan Comment feature in your CircleCI workflow, add the following to your `.circleci/config.yml`:

```yaml
version: 2.1

orbs:
  hterraform: helix/hterraform@x.y.z

workflows:
  terraform-workflow:
    jobs:
      - hterraform/plan-comment:
          # Optional: Customize parameters as needed
          terraform_dir: "path/to/terraform/dir"
          aws_role_arn: "arn:aws:iam::123456789012:role/your-oidc-role"
          use_aws_secret: true  # Set to false to use env vars instead of AWS Secrets
```

### Advanced Configuration

The `plan-comment` job and `terraform-plan-to-comment` command support several parameters for customization:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `terraform_dir` | Directory containing Terraform files | `.` |
| `plan_file_path` | Path to save terraform plan output | `/tmp/plan.txt` |
| `aws_role_arn` | ARN of the AWS IAM role to assume via OIDC | `""` |
| `aws_secret_name` | Name of the AWS secret containing GitHub token | `github/api-token` |
| `aws_region` | AWS region where the secret is stored | `us-east-1` |
| `use_aws_secret` | Whether to use AWS Secrets Manager or environment variables | `true` |
| `github_token_env` | Environment variable name for GitHub token | `GITHUB_TOKEN` |
| `custom_comment_prefix` | Custom prefix text for the GitHub PR comment | `### Terraform Plan Output` |

Example with custom parameters:

```yaml
- hterraform/plan-comment:
    terraform_dir: "./infrastructure"
    aws_role_arn: "arn:aws:iam::123456789012:role/custom-oidc-role"
    aws_secret_name: "custom/secret-path"
    aws_region: "us-west-2"
    custom_comment_prefix: "### Infrastructure Changes"
```

## Prerequisites

### Using AWS Secrets Manager (Default)

When using AWS Secrets Manager for GitHub tokens:

1. OIDC configuration requirements:
   - CircleCI must be configured as an OIDC identity provider in AWS IAM
   - The role specified in `aws_role_arn` must trust the CircleCI OIDC provider
   - For details on setting up OIDC with CircleCI, refer to the myhelix/oidc orb documentation

2. AWS IAM role requirements:
   - The role specified by `aws_role_arn` must have permissions to read from AWS Secrets Manager
   
3. AWS Secret format:
   - The secret should be stored in JSON format with a `token` field: `{"token": "your-github-token"}`

### Using Environment Variables

When not using AWS Secrets Manager:

1. Set `use_aws_secret: false` in your job configuration
2. Provide the GitHub token as an environment variable (default: `GITHUB_TOKEN`)

## License

See [LICENSE](LICENSE) file for details.
