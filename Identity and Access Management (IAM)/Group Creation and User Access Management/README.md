# AWS IAM Group Creation and User Access Management

## Project Overview

This project demonstrates the practical implementation of AWS Identity and Access Management (IAM) Groups to simplify user permission management using a Role-Based Access Control (RBAC) approach.

Instead of assigning permissions directly to individual users, IAM Groups were created for different departments, and AWS managed policies were attached at the group level. Users inherited permissions automatically based on their assigned group, reflecting how access management is implemented in enterprise cloud environments.

---

# Project Objective

The objective of this project was to gain hands-on experience in implementing scalable and secure access management using AWS IAM Groups.

This lab focuses on reducing administrative overhead, improving permission consistency, and following AWS security best practices by managing access through groups rather than individual users.

---

# Lab Environment

* Cloud Provider: AWS
* Service: AWS Identity and Access Management (IAM)
* Access Method: AWS Management Console
* Permission Model: Role-Based Access Control (RBAC)
* Policy Type: AWS Managed Policies

---

# Business Scenario

A fictional organization, **MinzTech**, requires different levels of AWS access for multiple teams based on their responsibilities.

To meet these requirements, dedicated IAM Groups were created, and appropriate AWS managed policies were assigned to each group.

This approach ensures that users receive only the permissions required for their specific job roles while maintaining centralized permission management.

---

# IAM Groups Implemented

### Developers-Team

Assigned Policies:

* AmazonEC2FullAccess
* AmazonS3FullAccess

Purpose:

Allows developers to manage EC2 instances and Amazon S3 resources without administrative access to other AWS services.

---

### Support-Team

Assigned Policy:

* AmazonS3ReadOnlyAccess

Purpose:

Allows support engineers to view S3 objects while preventing modifications or access to unrelated AWS services.

---

### Admins-Team

Assigned Policy:

* AdministratorAccess

Purpose:

Provides unrestricted administrative access for cloud administrators responsible for managing the AWS environment.

---

# User Assignment

The following IAM users were created and assigned to their respective groups.

| IAM User     | Assigned Group  | Permission Level           |
| ------------ | --------------- | -------------------------- |
| rahul-dev    | Developers-Team | EC2 and S3 Management      |
| amit-support | Support-Team    | Read-Only S3 Access        |
| prem-admin   | Admins-Team     | Full Administrative Access |

Because permissions are inherited from the assigned group, no policies were attached directly to individual users.

---

# Project Workflow

### Step 1 – Open AWS IAM Console

Accessed the AWS Management Console and navigated to the IAM service.

[Step 1](step%201.png)

---

### Step 2 – Create IAM Groups

Created separate IAM Groups for each department based on business requirements.

[Step 2](step%202.png)

---

### Step 3 – Attach AWS Managed Policies

Attached the required AWS Managed Policies to each IAM Group according to the required access level.

[Step 3](step%203.png)-to-[Step 14](step-14.png)

---

### Step 4 – Create IAM Users

Created IAM users representing employees from different departments.

[Step 15](step-15.png)-to-[Step 16](step-16.png)

---

### Step 5 – Add Users to IAM Groups

Assigned each user to the appropriate IAM Group.

Users automatically inherited all permissions associated with their assigned group.

[Step 17](step-17.png)-to-[Step 29](step-29.png)

---

### Step 6 – Verify Effective Permissions

Logged in using each IAM user account and validated the assigned permissions.

Verification included confirming both allowed operations and access restrictions.

---

# Permission Validation

The configured permissions were verified through practical testing.

### Support User

Verified:

* Amazon S3 Read-Only Access

Restricted:

* EC2 Management
* IAM Administration

---

### Developer User

Verified:

* Launch and manage EC2 instances
* Access Amazon S3

Restricted:

* IAM Administration
* Billing Management

---

### Administrator User

Verified:

* Full access to AWS services
* IAM administration
* Infrastructure management

---

# Security Best Practices Implemented

During this project, the following AWS security principles were applied:

* Role-Based Access Control (RBAC)
* Principle of Least Privilege
* Group-Based Permission Management
* Centralized Access Control
* AWS Managed Policies
* Avoided Direct Policy Attachment to Users
* Scalable Permission Administration

---

# Skills Demonstrated

* AWS Identity and Access Management (IAM)
* IAM Group Administration
* User Access Management
* Role-Based Access Control (RBAC)
* AWS Managed Policies
* Permission Inheritance
* Cloud Security Fundamentals
* Enterprise Identity Management
* AWS Management Console
* Access Verification and Testing

---

# Key Learnings

Through this hands-on implementation, I gained practical experience in:

* Creating and managing IAM Groups
* Assigning permissions through AWS Managed Policies
* Managing users using group-based access control
* Understanding permission inheritance
* Implementing least-privilege access
* Validating effective permissions using multiple IAM users
* Designing scalable IAM structures suitable for enterprise environments

---

# Project Outcome

This project successfully demonstrates how AWS IAM Groups simplify permission management in organizations by centralizing access control at the group level.

The implementation reflects a real-world enterprise identity management model where permissions are assigned based on job responsibilities rather than individual users. This approach improves scalability, reduces administrative effort, and supports secure cloud operations by ensuring consistent and controlled access across teams.

---

# Production Best Practices

* Assign permissions to IAM Groups instead of individual users.
* Follow the Principle of Least Privilege.
* Create separate groups for each business role.
* Use AWS Managed Policies where appropriate and Customer Managed Policies for fine-grained access.
* Regularly review group memberships and attached policies.
* Enable Multi-Factor Authentication (MFA) for privileged accounts.
* Monitor IAM activities using AWS CloudTrail for auditing and compliance.

---

# Screenshots

This repository includes step-by-step screenshots covering the complete implementation process, including:

* IAM Group Creation
* AWS Managed Policy Assignment
* IAM User Creation
* User-to-Group Assignment
* Permission Verification
* Access Validation for Different User Roles

Each screenshot documents a stage of the implementation and demonstrates the successful configuration of group-based access management in AWS IAM.
