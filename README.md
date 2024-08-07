# launching-a-scalable-application-in-aws-cloudformation
Launching a Scalable Web Application on AWS: A Case Study by IaaC- Cloud Formation

# XYZ Corporation: Scalable Web Application Deployment on AWS

## Table of Contents
- [Introduction](#introduction)
- [Architecture Overview](#architecture-overview)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
  - [1. VPC Setup](#1-vpc-setup)
  - [2. Web Tier Configuration](#2-web-tier-configuration)
  - [3. Application Tier Configuration](#3-application-tier-configuration)
  - [4. Database Tier Configuration](#4-database-tier-configuration)
  - [5. Route 53 Setup](#5-route-53-setup)
- [Usage](#usage)
- [Troubleshooting](#troubleshooting)
- [Conclusion](#conclusion)
- [Contact](#contact)

## Introduction
This project outlines the steps required to deploy a scalable, secure, and resilient web application on AWS. The solution leverages AWS CloudFormation to automate the provisioning and configuration of the infrastructure, enabling the development team to independently manage the environment without the need for system admins.

## Architecture Overview
The architecture consists of three main tiers:
1. *Web Tier*: An EC2 instance in a public subnet, accessible via HTTP (port 80) and SSH (port 22) from the internet.
2. *Application Tier*: An EC2 instance in a private subnet, accessible via SSH (port 22) only from the public subnet of the web tier.
3. *Database Tier*: An RDS MySQL instance in a private subnet, accessible on port 3306 only from the private subnet of the application tier.

Additionally, AWS Route 53 is configured to direct traffic to the EC2 instance in the web tier.

## Prerequisites
- AWS account with sufficient permissions to create the necessary resources.
- A key pair for SSH access to EC2 instances.
- Basic knowledge of AWS services (EC2, RDS, VPC, Route 53) and CloudFormation.

## Setup Instructions

### 1. VPC Setup
1. Create a VPC with a CIDR block of 10.0.0.0/16.
2. Create public and private subnets within the VPC:
   - Public Subnet: 10.0.1.0/24
   - Private Subnet: 10.0.2.0/24
3. Attach an Internet Gateway to the VPC.
4. Create a NAT Gateway and attach to Route table of private subnet
5. Configure route tables for public subnet.

### 2. Web Tier Configuration
1. Launch an EC2 instance in the public subnet.
2. Create and attach a security group that allows inbound traffic on HTTP (port 80) and SSH (port 22) from the internet.

### 3. Application Tier Configuration
1. Launch an EC2 instance in the private subnet.
2. Create and attach a security group that allows inbound SSH (port 22) traffic only from the public subnet of the web tier.

### 4. Database Tier Configuration
1. Launch an RDS MySQL instance in the private subnet.
2. Create and attach a security group that allows inbound MySQL (port 3306) traffic only from the private subnet of the application tier.
3. Ensure the RDS instance has a DeletionPolicy of Retain.

### 5. Route 53 Setup
1. Create a Route 53 hosted zone.
2. Set up an A record to direct traffic to the EC2 instance’s public IP address in the web tier.

## Usage
1. Deploy the CloudFormation stack using the provided template.
2. Access the web application via the Route 53 domain.
3. Connect to EC2 instances using the SSH key pair for configuration and troubleshooting.
4. Test and deploy your application code on the EC2 instances.

## Troubleshooting
- *EC2 Instance Connection Issues*: Ensure the security groups and network ACLs are correctly configured.
- *RDS Connectivity Issues*: Verify the security group rules and subnet configurations.
- *Route 53 Configuration*: Double-check the DNS records and ensure they point to the correct IP addresses.

## Conclusion
This project demonstrates how to use AWS services and CloudFormation to deploy a scalable and secure web application. By automating the infrastructure provisioning, the development team can focus on testing and deploying their code without relying on system admins.

## Contact
For any questions or further assistance, please contact:

- *Name*: Rizvana Begum
- *Email*: rizvanabegumt@outlook.com
- *LinkedIn*: www.linkedin.com/in/rizvanabegum


