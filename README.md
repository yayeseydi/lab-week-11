# 4640-ansible-roles-lab



## Getting started

See D2L for lab instructions.
This repository contains the completed Week 11 Ansible Roles Lab.  
The objective of the lab was to refactor an existing Ansible configuration into a role-based structure, deploy two AWS EC2 instances using Terraform, and configure them using Ansible with a dynamic AWS inventory.

---

## Repository Structure

.
├── README.md
├── server-img.jpg
├── ansible/
│ ├── ansible.cfg
│ ├── playbook.yml
│ ├── inventory/
│ │ └── aws_ec2.yml
│ └── roles/
│ ├── frontend/
│ │ ├── tasks/main.yml
│ │ ├── handlers/main.yml
│ │ ├── templates/index.html.j2
│ │ └── files/default.conf
│ └── redis/
│ └── tasks/main.yml
├── terraform/
│ ├── main.tf
│ ├── provider.tf
│ └── modules/web-server/
│ ├── main.tf
│ ├── outputs.tf
│ └── variables.tf
└── scripts/
├── import_lab_key
└── delete_lab_key

yaml
Copy code

---

## SSH Key Setup

Create a new SSH key for AWS:

```
ssh-keygen -t ed25519 -f ~/.ssh/aws
```
Add the key to your AWS account:

```
cd scripts
./import_lab_key
```
### Terraform Deployment
Provision the two EC2 servers:
```
cd terraform
terraform init
terraform apply
```
The dynamic inventory in Ansible will automatically detect the new servers.

### Ansible Configuration
After provisioning, run the playbook:
```
cd ../ansible
ansible-playbook -i inventory/aws_ec2.yml playbook.yml
```
### This playbook performs the following:

Installs and configures NGINX on the Ubuntu frontend server

Creates and deploys an HTML template

Installs Redis on the Rocky Linux server

Uses handlers to reload NGINX when configuration files change

Uses the AWS EC2 dynamic inventory plugin


The screenshot shows the HTML page served by the Ubuntu frontend server:

