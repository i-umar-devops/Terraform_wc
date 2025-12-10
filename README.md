# Terraform AWS Infrastructure – Project

This repository contains a Terraform configuration that provisions a basic AWS infrastructure end‑to‑end. It demonstrates my hands‑on experience with Infrastructure as Code on AWS, including use of remote state, variables, key pairs, and repeatable environment creation.

## What this project does

- Uses Terraform to create AWS resources from scratch (based on a chosen AMI ID).
- Manages configuration via `variables.tf` and `config.tf` for easy reuse across environments.
- Automates key creation and secure SSH access to EC2 instances.
- Provides a simple, reproducible workflow: `init` → `plan` → `apply` → `destroy`.

## Prerequisites

- Terraform installed  
- AWS account and IAM user with programmatic access  
- AWS CLI installed and configured  
- Python installed (if needed for helper scripts or tooling)

Useful links (official docs):

- Terraform: https://www.terraform.io/downloads  
- Python: https://www.python.org/downloads/  
- AWS CLI install: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html  
- AWS console (for access keys / S3 bucket): https://aws.amazon.com/console/

## Configuration steps

1. **Update AMI and SSH key path**

   - Find a suitable AMI ID in your AWS region and set it in `variables.tf`.
   - Generate an SSH key pair and update `PUBLIC_KEY_PATH` in `variables.tf` with the full path:
     ```
     ssh-keygen -f oregon-region-key-pair
     ```
     This creates `oregon-region-key-pair` and `oregon-region-key-pair.pub`.

2. **Configure AWS credentials**

   - Create an access key for your IAM user in the AWS Console.
   - Configure the AWS CLI:
     ```
     aws configure
     ```
   - Ensure the region matches the one used in the Terraform files.

3. **Remote state / S3 bucket**

   - Create an S3 bucket for Terraform state.
   - Add the bucket name (and region) in `config.tf` as required by your backend configuration.

4. **Review variables and config**

   - Adjust values in `variables.tf` and `config.tf` (e.g. region, instance type, tags) to match your environment.
