This project uses **Terraform** to provision an **Amazon EC2** instance running **NGINX**. It automates the creation of an EC2 instance, sets up SSH and HTTP access, installs NGINX on boot, and serves a simple web page. This is a foundational DevOps project for learning infrastructure as code (IaC) on AWS.

## Stack

- **Terraform**  
- **AWS EC2 (Amazon Linux 2)**  
- **NGINX**  
- **SSH Key Pair**  
- **Security Group (ports 22 and 80)**  

## What It Does

- Creates a t2.micro EC2 instance in the `us-east-2` region  
- Sets up a security group that allows:
  - SSH access on port 22  
  - HTTP access on port 80  
- Uses a local SSH public key (`/home/nikola/.ssh/id_rsa.pub`)  
- Installs NGINX automatically via user data script  
- Serves a basic HTML page  
- Outputs the instance's public IP after deployment  

## File Structure

.
├── main.tf # Terraform config: instance, SG, key, user_data
├── outputs.tf # Output for EC2 public IP
├── .gitignore # Files to ignore in version control
└── README.md # Project documentation


## Prerequisites

- [Terraform](https://developer.hashicorp.com/terraform/downloads) installed  
- AWS CLI configured (`aws configure`)  
- SSH key pair already created:  
  - Public key located at: `/home/nikola/.ssh/id_rsa.pub`  

## How to Deploy

1. Clone this repository

```bash
git clone https://github.com/NikolaKitanovicTF/ec2-nginx-setup.git
cd ec2-nginx-setup

Initialize Terraform

terraform init

Review the execution plan

terraform plan

Apply the configuration

terraform apply

Confirm with yes when prompted.

 Access your NGINX server

Once Terraform finishes, it will output the public IP:

Outputs:

public_ip = "<your-ec2-public-ip>"

Open your browser and visit:

http://<public_ip>

Output

The outputs.tf file provides the public IP automatically after deployment:

output "public_ip" {
  description = "Public IP of the EC2 instance"
  value       = aws_instance.nginx_server.public_ip
}

Clean Up Resources

To destroy everything and avoid unwanted AWS charges:

terraform destroy

.gitignore

To protect sensitive data and avoid committing unnecessary files:

# Ignore Terraform state and cache
.terraform/
*.tfstate
*.tfstate.backup

# Ignore SSH keys and sensitive files
*.pem
*.key
*.pub
id_rsa
id_rsa.pub

Notes

The security group allows access from 0.0.0.0/0 — good for testing, not secure for production.

Author

Nikola Kitanovic
GitHub: NikolaKitanovicTF
License

This project is licensed under the MIT License.
