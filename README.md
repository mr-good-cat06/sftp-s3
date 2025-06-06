# managed-secure-sftp-using-terrafrom


### Purpose
Terraform stack to deploy an S3 Bucket backed SFTP server (Based on the **AWS Transfer Family** service) in AWS using static IP addresses that will restrict incoming connections to specific IP ranges. Authentication is password based using AWS Lambda for validation with passwords stored in AWS Secrets Manager. **Please see the note below in the Cleanup section that setting up this SFTP server will cost you real money - there is no free tier!!**

![1](https://github.com/user-attachments/assets/284363d7-d1ae-445d-9356-2a3ed3b3be3f)


### Key Folders

- `terraform` - Contains all the files in the Terraform stack to deploy everything in the backend including the AWS Lambda Function, S3 Buckets, Secrets Manager secrets, AWS Transfer Family SFTP server, and more.
- `functions` - Source code for the Python function used to authenticate user login to the SFTP server

### Requirements

-   Terraform CLI (https://developer.hashicorp.com/terraform/install)

### Deploy the project

To deploy the project, you need to do the following:

1. Clone the repo
2. Go to the terraform directory
3. Make changes to the `configuration.tf` file to setup which incoming IP CIDR ranges should be allowed access to the server, the sftp user name, which AWS region to use, and other values.
4. Run `terraform init`
5. run `terraform apply` (and type "yes" when it's done with the plan)
6. Note the output from the terraform apply. It will contain the static IP addresses where the SFTP server is running, the password for the sftp server, and the S3 bucket which will contain all the files uploaded/downloadable for the sftp server.

### Cleanup

# **WARNING: If you leave the SFTP server running and do not destroy it with Terraform then you will incur real costs in $$$s. AWS Transfer Family SFTP servers cost 7 USD per day (plus bandwidth charges)!!!**


Run the following terraform command to destroy all the infrastructure.

```bash
terraform destroy (from the infra directory)
```


