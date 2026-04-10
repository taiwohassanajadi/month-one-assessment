#  Alt School Africa - Month-One-Assessment
Alt School Africa-Month one assessment, the project involved building a secure and reliable "home" on the internet for TechCorp's new web application.


TechCorp Web Infrastructure Deployment with Terraform

📌 Project Overview
This repository contains the Infrastructure as Code (IaC) solution for TechCorp’s web application. The goal of this project was to move away from manual cloud configuration and embrace automation to ensure a secure, scalable, and highly available environment.
While the initial requirements were modeled for AWS, this deployment was executed on Google Cloud Platform (GCP). I have successfully mapped all requested AWS components to their GCP equivalents, demonstrating cloud-agnostic engineering skills and technical adaptability.

🏗️ Architecture Design

The infrastructure is designed to survive component failures and protect sensitive data through a multi-layered network approach:
Virtual Private Cloud (VPC): A custom network named techcorp-vpc providing complete isolation.
Multi-Zone Subnets: Four subnets distributed across different zones to ensure High Availability (HA).
Public Subnets: Hosting the Load Balancer entry points.
Private Subnets: Hosting the Web Servers and Database to prevent direct internet exposure.
Global HTTP Load Balancer: Acts as a traffic manager, distributing incoming requests between healthy web servers.
Cloud NAT & Router: Enables private servers to download security updates without being assigned a public IP address.
Managed Firewall Rules: Strict "Least Privilege" access, allowing only necessary traffic (HTTP/HTTPS/SSH).




📂 Repository Structure

Plaintext

month-one-assessment/
├── main.tf                 # Core resource definitions (VPC, Instances, LB)
├── variables.tf            # Input variable declarations
├── outputs.tf              # Final deployment data (Load Balancer IP)
├── terraform.tfvars.example # Template for required environment variables
├── user_data/
│   ├── web_server_setup.sh  # Script to automate Apache installation
│   └── db_server_setup.sh   # Script to automate PostgreSQL installation
├── evidence/               # Folder containing deployment screenshots
└── README.md               # Project documentation


⚙️ Technical Mapping (AWS to GCP)

Business Requirement
AWS Service
GCP Equivalent (This Project)
Isolated Network
VPC
google_compute_network
Public/Private Subnets
Subnets
google_compute_subnetwork
Security Groups
Security Groups
google_compute_firewall
Compute Instances
EC2
google_compute_instance
Scalable Load Balancing
ALB
Global HTTP Load Balancer
Secure NAT
NAT Gateway
Cloud NAT + Cloud Router

🚀 Deployment Instructions

1. Prerequisites
Terraform is installed locally or using Google Cloud Shell.
A GCP Project with Billing and the Compute Engine API enabled.
2. Configuration
Create a terraform.tfvars file based on the example:

Bash

_cp terraform.tfvars.example terraform.tfvars
# Open terraform.tfvars and fill in your Project ID and IP_


3. Execution
Run the following commands in your terminal:

Bash

_terraform init      # Initialize the working directory
terraform plan      # Preview the changes
terraform apply     # Deploy the infrastructure (type 'yes' when prompted)_


4. Verification
Once complete, Terraform will output your Load Balancer IP. Paste this into your browser to see the live web servers.

🧪 Validating High Availability
To prove the system's reliability, I performed a Failover Test:
Stop Server 1: Manually shut down web-server-1 in the console.
Health Check: The Load Balancer detected the failure within seconds.
Automatic Routing: Traffic was immediately rerouted to web-server-2.
Result: The website stayed online with zero downtime for the user.

🧹 Cleanup
To avoid unnecessary cloud charges after grading, destroy all resources:

Bash

_terraform destroy_




👤 Author
Taiwo Hassan Ajadi AltSchool ID: ALT/SOE/025/4681 Cloud Engineering Track 📧 ajaditaiwo530@gmail.com
