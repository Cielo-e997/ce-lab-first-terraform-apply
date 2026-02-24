# Terraform Workflow — Lab M4.01

Region: eu-central-1  
Bucket: terraform-lab-bucket-cielo-170638199494

---

## terraform init

Initializes the working directory and downloads the AWS provider.
Creates the .terraform directory and lock file.

Result: Initialization successful.

---

## terraform validate

Checks the configuration syntax and internal consistency.

Result: Configuration was valid.

---

## terraform fmt

Formats Terraform files to standard style.

---

## terraform plan (Initial creation)

Showed that Terraform would create:
- aws_s3_bucket.lab_bucket
- aws_s3_bucket_versioning.lab_bucket

Plan: 2 to add, 0 to change, 0 to destroy.

---

## terraform apply

Created the S3 bucket and enabled versioning.

Result:
Apply complete! Resources: 2 added.

Outputs:
- bucket_arn
- bucket_name
- bucket_region

---

## Adding encryption

Added aws_s3_bucket_server_side_encryption_configuration.

terraform plan showed:
Plan: 1 to add, 0 to change, 0 to destroy.

terraform apply completed successfully.

---

## State exploration

terraform state list showed:
- aws_s3_bucket.lab_bucket
- aws_s3_bucket_versioning.lab_bucket
- aws_s3_bucket_server_side_encryption_configuration.lab_bucket

terraform state show confirmed:
- Versioning enabled
- Encryption set to AES256
- Region eu-central-1

---

## Inspecting terraform.tfstate

Command used:
cat terraform.tfstate | jq .

Observation:
The state file contains resource metadata (ARNs, region, bucket name).
This is why it should never be committed to Git.

---

## terraform destroy

Destroyed all resources at the end of the lab to avoid charges.
