# Create IAM User

## Project Overview

This hands-on lab demonstrates the process of creating and configuring an AWS Identity and Access Management (IAM) user for secure access to AWS resources. The implementation follows AWS security best practices by avoiding the use of the root account for daily administrative tasks and assigning permissions through IAM.

The project includes creating an IAM user, configuring AWS Management Console access, setting a custom password, assigning permissions, and validating successful user authentication.

---

# Objective

The objective of this lab was to understand how AWS IAM manages authentication and authorization by creating a dedicated IAM user with appropriate permissions.

This project helped me gain practical experience in user management, permission assignment, secure credential handling, and implementing cloud security best practices.

---

# Lab Environment

* Cloud Provider: AWS
* Service: Identity and Access Management (IAM)
* Access Method: AWS Management Console
* Region: Global Service
* User Type: IAM User

---

# Prerequisites

Before starting this lab, the following requirements were available:

* Active AWS Account
* Root User Access
* IAM Service Enabled
* Internet Browser

---

# Implementation Steps

## Step 1 – Sign in to AWS Management Console

Logged in using the AWS root account to perform the initial IAM configuration.

---

## Step 2 – Open IAM Service

Navigated to:

AWS Console → IAM

Verified that IAM is a global AWS service.

---

## Step 3 – Create a New IAM User

Created a new IAM user by providing:

* User Name
* AWS Management Console Access
* Programmatic Access (if required)

Configured the account according to the project requirements.

---

## Step 4 – Configure Console Password

Configured a secure password for the IAM user.

Performed the following:

* Created a custom password
* Enabled password reset during first login (if applicable)
* Verified password policy compliance

---

## Step 5 – Assign Permissions

Configured user permissions using AWS IAM.

Permission assignment methods available:

* Add user to existing group
* Copy permissions from another user
* Attach policies directly

For this implementation, the appropriate permission method was selected based on the lab objective.

---

## Step 6 – Review Configuration

Verified:

* User Name
* Console Access
* Assigned Permissions
* Password Configuration

Reviewed all settings before creating the IAM user.

---

## Step 7 – Create IAM User

Successfully created the IAM user.

AWS generated:

* Console Sign-In URL
* Username
* Login Information

These credentials were securely stored for testing purposes.

---

## Step 8 – Validate User Login

Signed out from the root account.

Logged in using the newly created IAM user.

Verified:

* Successful authentication
* Console accessibility
* Assigned permissions
* Dashboard visibility

---

# Security Considerations

During this implementation, the following AWS security practices were observed:

* Avoided using the Root Account for routine administrative tasks.
* Created a dedicated IAM user.
* Used a strong custom password.
* Followed the Principle of Least Privilege while assigning permissions.
* Verified successful authentication after account creation.

---

# Verification

The implementation was considered successful after confirming:

* IAM user created successfully.
* Console login completed without errors.
* Assigned permissions worked as expected.
* AWS Management Console was accessible using the new IAM credentials.

---

# Key Learnings

Through this lab, I gained practical experience with:

* AWS IAM User Management
* Authentication and Authorization
* AWS Console Access Configuration
* Password Management
* Permission Assignment
* Secure User Administration
* AWS Security Best Practices

---

# Skills Demonstrated

* AWS Identity and Access Management (IAM)
* User Administration
* Access Control
* Cloud Security Fundamentals
* AWS Management Console
* Authentication Management
* Permission Configuration
* Documentation and Technical Implementation

---

# Project Outcome

This lab provided hands-on experience in creating and managing IAM users within AWS. It strengthened my understanding of identity management, secure access control, and user administration, which are fundamental concepts for managing cloud environments.

The project also reinforced the importance of following AWS security best practices by minimizing root account usage and implementing controlled access through IAM.

---

## Production Best Practices

- Never use the AWS Root Account for daily operations.
- Assign permissions using IAM Groups whenever possible.
- Follow the Principle of Least Privilege.
- Enable Multi-Factor Authentication (MFA) for privileged users.
- Regularly review and rotate credentials.
- Avoid attaching AdministratorAccess unless absolutely necessary.
- Monitor IAM activities using AWS CloudTrail.
