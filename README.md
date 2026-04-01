# Terraform Zero to Hero

Hands-on Terraform learning repository with day-wise examples from fundamentals to modules, remote state, provisioners, workspaces, and secret management.

## What You Will Learn

- Terraform core concepts: providers, resources, variables, outputs, state, and plan/apply flow
- AWS infrastructure provisioning with Terraform
- Reusable modules and workspace-based environments
- Remote backend with S3 and DynamoDB locking
- Provisioners (`file`, `remote-exec`, `local-exec`) and app bootstrap flow
- Security practices for Terraform and Vault-based secret integration

## Prerequisites (All Requirements)

Before running any example in this repo, make sure you have:

- Terraform installed (latest stable recommended)
- AWS account
- AWS CLI installed and configured
- IAM user credentials with required permissions
- Git installed
- VS Code or any code editor

Optional (needed for specific days):

- SSH key pair in your local machine:
  - Linux/macOS: `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`
  - Windows (Git Bash): `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`
- Python 3 and pip (for day-05 Flask app provisioner example)
- HashiCorp Vault (for day-07 Vault integration example)

## Installation

### 1) Install Terraform

Install Terraform from the official downloads page:

- https://developer.hashicorp.com/terraform/downloads

### 2) Install and Configure AWS CLI

Install AWS CLI:

- https://aws.amazon.com/cli/

Configure credentials:

```bash
aws configure
```

You will be prompted for:

- AWS Access Key ID
- AWS Secret Access Key
- Default region
- Output format

## Quick Start

From any day folder that contains Terraform code:

```bash
terraform init
terraform plan
terraform apply
```

To destroy resources:

```bash
terraform destroy
```

## Repository Structure

```text
.
|-- main.tf
|-- day-01/
|   |-- 01-fundamentals.md
|   |-- 02-getting-started.md
|   |-- 03-install.md
|   |-- 04-aws-connection.md
|   `-- project-ec2-creation-day-01/
|-- day-02/
|-- day-03/
|-- day-04/
|-- day-05/
|-- day-06/
`-- day-07/
```

## Day-wise Learning Path

### Day 01 - Fundamentals + First EC2

- IaC basics and Terraform advantages
- Terraform terminology (provider, resource, module, variable, output, state)
- Terraform installation and AWS connection setup
- First EC2 creation walkthrough in `day-01/project-ec2-creation-day-01/`

### Day 02 - Providers, Variables, Expressions

- Provider configuration patterns
- Multiple providers and multiple region setup (using aliases)
- `required_providers` usage and version constraints
- Input/output variables and `.tfvars`
- Conditional expressions and built-in functions

### Day 03 - Modules

- Why modules are useful (reusability, maintainability)
- Module consumption from root configuration
- Sample custom module in `day-03/modules/ec2_instance/`

### Day 04 - State and Remote Backend

- Terraform state file concepts and caveats
- S3 backend configuration in `day-04/backend.tf`
- DynamoDB state locking example in `day-04/main.tf`

### Day 05 - Provisioners + App Bootstrap

- Network and EC2 setup for provisioning
- `file` provisioner to copy app code (`app.py`)
- `remote-exec` for package install and app startup
- Provisioner concepts documented in `day-05/provisioners.md`

### Day 06 - Workspaces + Environment Mapping

- `terraform.workspace` usage
- Map lookup pattern for env-based instance type selection
- Variable injection from `terraform.tfvars`

### Day 07 - Secure Terraform + Vault

- Handling sensitive values and secure patterns
- Vault provider integration example
- Reading secret values and using them in resource attributes

## Important Notes Before Running Examples

- Several Terraform files contain placeholder comments like `# change this`.
  Update AMI IDs, subnet IDs, bucket names, key names, regions, and other values before `apply`.
- Keep S3 bucket names globally unique.
- Never commit real secrets, access keys, or private keys.
- Do not commit local state with sensitive information in real projects.

## Recommended Safe Workflow

```bash
terraform fmt
terraform validate
terraform plan
terraform apply
```

## Security Best Practices

- Use least-privilege IAM policies
- Prefer remote state with encryption and locking
- Store secrets in Vault / secret manager / environment variables
- Mark sensitive Terraform values as `sensitive = true` where applicable

## Troubleshooting

- `No valid credential sources found`:
  - Re-run `aws configure`
  - Check environment variables and AWS profile
- `Invalid AMI ID`:
  - Use a region-valid AMI for your selected AWS region
- `BucketAlreadyExists`:
  - Rename the S3 bucket to a globally unique value
- SSH/provisioner failures:
  - Verify key path, security group ingress, subnet routing, and instance user

## Useful References

- Terraform Docs: https://developer.hashicorp.com/terraform/docs
- AWS Provider Docs: https://registry.terraform.io/providers/hashicorp/aws/latest/docs
- Vault Provider Docs: https://registry.terraform.io/providers/hashicorp/vault/latest/docs

## Disclaimer

This repository is for learning/demo purposes. Validate and harden every configuration before using in production.