# Terraform

# Table of Content:
- [Requirements](#requirements)
- [What is Terraform?](#what-is-terraform-(windows))
- [Installing Terraform Windows](#installing-terraform---windows)
- [Installing Terraform - Linux](#installing-terraform---linux)
- [Create AWS IAM use](#create-aws-iam-use)
- [Creating Config file using the credentials csv file](#creating-config-file-using-the-credentials-csv-file)
- [Init git working directory](#init-git-working-directory)
- [Terraform apply](#terraform-apply)

---


## Requirements
- [AWS Account](https://aws.amazon.com/account/)
- Git
- Basics in System administration and networking basics


## What is Terraform?
- Infrastructure management tool made by [HashiCorp](https://www.hashicorp.com)
- Provision, manage, and maintain cloud resources like servers, networking, storage. 
- Terraform is for managing the base infrastructure *Not a configuration Management System*
- Terraform works with Docker, Kubernetes, Cloud. 
![terraformexecution](/assets/terraformexecutionplan.png)
![terraformflow](/assets/terraformflow.png)
 

## Installing Terraform - Windows
- Visit [Terraform Download CLI](https://www.terraform.io/downloads.html) > choose the operating system.
- Choose folder to download in `%USERPROFILE%\bin`    *create bin folder if not available*
- Extract the file into `%USERPROFILE%\bin`
- Search for `Enviroment Variable` on your machine > click `Environment Variables...` on User variables for "your-user" highlight `Path` click `New` type into the field `%USERPROFILE%\bin` click `OK` then `OK` then `OK` to exit Environment Variables.
- Open a new PowerShell and type `terraform` to check if Terraform was inserted into your Path correctly. 
![installing_terraform_windows](/assets/installing_terraform_windows.gif)
- Visit [Install Terraform Documentation](https://learn.hashicorp.com/tutorials/terraform/install-cli) 


## Installing Terraform - Linux
- `wget https://releases.hashicorp.com/terraform/0.14.6/terraform_0.14.6_linux_amd64.zip`   *64-bit*  [Terraform Download CLI](https://www.terraform.io/downloads.html)
- `unzip terraform_0.14.6_linux_amd64.zip`
- `sudo mv terraform /bin`
- `rm terraform_0.14.6_linux_amd64.zip`
- `terraform --version`


## Create AWS IAM use
- Login to [AWS Account](https://aws.amazon.com/account/)
- Click `Users` on Dashboard then `Add user`
- Insert a username. Example `terraform`
-  Select AWS access type `Programmatic access`
-  Go next select `Attach existing policies directly` then check `AdministratorAccess`  *this is bad practice and should be avoided if you know what policies to assign your username to use terraform*
-  Click Next and Review
-  Download the .CSV file containing the credentials


## Creating Config file using the credentials csv file
- Open credential file from previous step and edit using vscode
- Delete the first line containing headings
- Delete username comma and password field
- Delete the website at the end
- Add `[default]` at the beginning of the file
- Add before Access key ID `aws_access_key_id=`
- Add before Secret access key `aws_secret_access_key=`
- Save in `%USERPROFILE%\.aws\credentials`    *credentials file has no extension so make sure it don't have via the command line*
![credentials example](/assets/credentails.png)
- `mv new_user_credentials.csv credentials`


## Init git working directory
- Open GitBash and type command `mkdir ~/Desktop/terraform`
- `cd ~/Desktop/terraform` then init git by `git init`
- Create file first_code.tf by command `vim first_code.tf`
![first_code](/assets/first_code.png)
- To change the default location of the credentials file use `shared_credentials_file = "credentials path"` beneath `region = "us-west-2"` in `first_code.tf` file
- Add terraform to .gitignore (Important security mesurement) 
    - .gitignore can be downloaded or forked from this repo
    - Contains windows/linux/mac/terraform
    - Create your own via [Toptal](https://www.toptal.com/developers/gitignore)
- `git add *` then `git commit -m "init commit and config file"`
- `terraform init`  
![terraform_init](/assets/terraform_init.png)
- `git push`


## Terraform apply
- executing `terraform apply` will generate a plan and prompt to execute.
![commandline](/assets/terraformapply.png)
![amazon_account](/assets/amazonterraformapply.png)
