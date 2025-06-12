# minecraft-server-automation

This project works to automate and configure a Minecraft server on an AWS EC2 instance by using Terraform and Ansible.

# Operating System

The operating system that is used is Linux or WSL2, which is a Windows Subsystem for Linux

# Tools

Terraform is used, must be version v1.5 or greater

Ansible is used, must be version v2.14 or greater

AWS CLI is used, must be version v2.0 or greater

SSH key pair is used for EC2 access

Git is used

# AWS

You must have an AWS Account with access keys properly configured. You also need to have EC2 instance permissions as well as access to VPCs and Security Groups.

# Project Overview

### 1. Terraform Infrastructure
- This project creates an EC2 instance with a specific key pair
- It has open ports on 25565 for Minecraft and Port 22 for SSH
- The outputs and the public IP address are needed for the instance


### 2. Ansible Configuration
- This install Java (In this instance I used Amazon Corretto 21)
- It creates a directory named 'minecraft'
- It downloads the most recent minecraft server file, as well as accepts the EULA
- It configures and starts the Minecraft server with 'systemd'

# Tutorial on how to run

We will go in a step-by-step process, so just follow each respective number below

1. Start off by cloning the repository by running these commands:
git clone https://github.com/Ryan-Giard/minecraft-server-automation.git
cd minecraft-server-automation

2. Then Install terraform and get it to run. Make a directory for terraform.

cd terraform
terraform init
terraform apply (you will be prompted to enter something, type yes)

Note down the public IP that it gives you

3. Copy your private key into ~/.ssh/ and run chmod 400 on it.

4. You can then run ansible like this:
cd ../ansible
ansible-playbook -i inventory.ini playbook.yml

5. Connect to the server from here!

Go to your minecraft client, and run this command to check the port status

nmap -sV -Pn -p T:25565 (IP)

