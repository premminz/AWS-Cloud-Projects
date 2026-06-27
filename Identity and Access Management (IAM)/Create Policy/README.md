# Create Custom IAM Policy for Secure Amazon S3 Access

## Project Overview

This project demonstrates the design and implementation of a custom AWS Identity and Access Management (IAM) policy to provide controlled access to an Amazon S3 bucket. The primary objective was to implement the Principle of Least Privilege by allowing users to perform only the required actions while restricting access to all other AWS resources.

As part of this hands-on lab, I created a custom IAM policy using the JSON policy editor, attached the policy to an IAM Group, assigned an IAM User to the group, and validated that the configured permissions behaved as expected.

---

# Project Objective

The objective of this project was to gain practical experience in designing and implementing custom IAM policies instead of relying solely on AWS managed policies.

This implementation focused on securing Amazon S3 resources by granting only the minimum permissions required for business operations while preventing unauthorized access to other AWS services.

---

# Lab Environment

* Cloud Provider: AWS
* Service: AWS Identity and Access Management (IAM)
* Storage Service: Amazon S3
* Policy Type: Customer Managed Policy
* Permission Model: Least Privilege
* Access Method: AWS Management Console

---

# Project Architecture

```text
IAM User
      │
      ▼
IAM Group
      │
      ▼
Custom IAM Policy (JSON)
      │
      ▼
Amazon S3 Bucket
```

The IAM User receives permissions through group membership rather than direct policy attachment, following AWS security best practices.

---

# Technologies and AWS Services Used

* AWS IAM
* Amazon S3
* IAM Groups
* Customer Managed Policies
* JSON Policy Editor
* AWS Management Console

---

# Implementation Workflow

### Step 1 – Create an Amazon S3 Bucket

Created a dedicated S3 bucket that would be used to test access permissions.

**Screenshot:** [Step 1](step%201.png)

---

### Step 2 – Create a Customer Managed IAM Policy

Created a new IAM policy using the JSON editor.

The policy was designed to:

* Allow bucket listing
* Allow object upload
* Allow object download
* Restrict access to every other bucket
* Restrict access to unrelated AWS services

**Screenshots:** [Step 2](step%202.png) – [Step 10](step-10.png)

---

### Step 3 – Validate the JSON Policy

Validated the policy syntax and confirmed that all permissions were correctly configured before creating the policy.

**Screenshots:** [Step 11](step-11.png) – [Step 13](step-13.png)

---

### Step 4 – Create an IAM Group

Created an IAM Group and attached the newly created custom policy.

Using groups instead of assigning permissions directly to users simplifies administration and follows AWS recommended practices.

**Screenshots:** [Step 14](step-14.png) – [Step 17](step-17.png)

---

### Step 5 – Create an IAM User

Created a new IAM user with AWS Management Console access and added the user to the IAM Group.

The user automatically inherited all permissions defined by the attached custom policy.

**Screenshots:** [Step 18](step-18.png) – [Step 22](step-22.png)

---

### Step 6 – Verify Access Permissions

Signed in using the IAM user credentials and validated the configured permissions.

Verified that the user could:

* View the designated S3 bucket
* Upload objects
* Download objects

Verified that the user could **not**:

* Access other S3 buckets
* Delete the bucket
* Access IAM administrative functions
* Access unrelated AWS services

**Screenshots:** [Step 23](step-23.png) – [Step 25](step-25.png)

---

# Security Best Practices Implemented

During this project, the following AWS security practices were followed:

* Created a Customer Managed IAM Policy
* Applied the Principle of Least Privilege
* Granted only required permissions
* Used IAM Groups instead of attaching policies directly to users
* Restricted access to a specific S3 bucket
* Avoided unnecessary administrative permissions
* Validated permissions through practical testing

---

# Skills Demonstrated

* AWS Identity and Access Management (IAM)
* IAM Policy Design
* JSON Policy Configuration
* Amazon S3 Access Control
* Role-Based Access Management
* IAM Group Administration
* Principle of Least Privilege
* Cloud Security Fundamentals
* Access Verification and Testing
* AWS Management Console

---

# Key Learnings

Through this project, I developed a practical understanding of:

* How IAM policies control access to AWS resources
* The difference between AWS Managed and Customer Managed Policies
* Writing and validating JSON-based IAM policies
* Assigning permissions using IAM Groups
* Implementing least-privilege access in real-world cloud environments
* Verifying policy behavior by testing allowed and denied operations

---

# Project Outcome

This project successfully demonstrated how to implement secure and scalable access control within AWS using Customer Managed IAM Policies.

Rather than granting broad administrative permissions, access was limited to a specific Amazon S3 bucket, ensuring users could perform only the actions required for their responsibilities. This approach aligns with AWS security best practices and reflects how access control is commonly implemented in production cloud environments.

---

# Screenshots

This repository includes step-by-step screenshots covering:

* S3 Bucket Creation
* Custom Policy Creation
* JSON Policy Configuration
* Policy Validation
* IAM Group Creation
* IAM User Creation
* Policy Attachment
* User Login
* Permission Verification
* S3 Access Testing

Each screenshot corresponds to the implementation sequence followed during the practical lab.
