1. Create IAM User
    IAM ->> Create User ->> "Username" ->> Attach policies directly (AmazonEC2FullAccess) ->> Create user.

2. Create an Access key for the User
    User ->> Security credentials ->> Create Access Key ->> Use case: Command Line Interface (CLI) ->> Create Access Key ->> 
    Download .csv file

3. Launch an EC2 Instance and connect using SSH

4. Install AWS-CLI and Configure AWS
   Commands:
   sudo yum install awscli -y
   aws --version
   aws configure

5. Enter Access Key (mentioned in CSV file), Secret Access Key (mentioned in CSV file), Region-name and Output Format (json)

6. Install Terraform
   Commands:
   sudo yum install -y yum-utils shadow-utils
   sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
   sudo yum -y install terraform
   terraform --version

7. Create a Project directory and .tf file
   Commands:
   mkdir Project
   cd Project
   touch main.tf
   sudo nano main.tf

8. Add the code below in main.tf file:

   terraform {
     required_providers {
       aws = {
         source = "hashicorp/aws"
         version = "5.66.0"
       }
     }
   }
  
   provider "aws" {
     region = "us-east-1"
   }
  
   resource "aws_instance" "webserver" {
     ami           = "ami-0182f373e66f89c85"
     instance_type = "t2.micro"
  
     tags = {
       Name = "Terraform-Instance"
     }
   }


9. Save the main.tf file and execute the commands below:
   Commands:
   terraform init
   terraform plan
   terraform apply

10. Check the AWS Console to verify that a new EC2 instance has been created

11. Execute the command to terminate the Terraform Instance
    Command:
    terraform destroy

    You will notice the EC2 instance is terminated.
