# Amazon Machine Image (AMI)

## Overview

This section contains my hands-on AWS Amazon Machine Image (AMI) projects focused on building reusable, secure, consistent, and scalable EC2 infrastructure.

Through these practical implementations, I explored the complete AMI lifecycle — from creating a custom AMI from a configured EC2 instance to securing and reusing the image, replicating it across AWS Regions, and integrating it with Auto Scaling Groups for automated and self-healing infrastructure.

These projects demonstrate how AMIs can be used to standardize EC2 deployments and reduce manual configuration effort in cloud environments.

---

# Learning Objectives

Through these hands-on projects, I gained practical experience in:

* Creating custom AMIs from configured EC2 instances
* Preparing EC2 instances before creating reusable images
* Installing and configuring applications within an AMI
* Applying security and system-hardening practices
* Launching new EC2 instances from custom AMIs
* Copying AMIs between AWS Regions
* Understanding AMI and EBS snapshot relationships
* Using custom AMIs with Launch Templates
* Integrating AMIs with Auto Scaling Groups
* Building self-healing EC2 infrastructure
* Implementing Golden AMI strategies
* Designing infrastructure for availability and disaster recovery

---

# AWS Services Used

* Amazon EC2
* Amazon Machine Image (AMI)
* Amazon EBS
* Launch Templates
* Auto Scaling Groups
* Amazon VPC
* AWS Security Groups
* SSH
* Multiple AWS Regions

---

# Projects Included

## 1. Create Custom AMI from EC2 Instance

### Objective

Created a custom Amazon Machine Image from a pre-configured EC2 instance containing an Apache Web Server.

The custom AMI was then used to launch a new EC2 instance with the same operating system, application, and configuration.

### Key Concepts

* Custom AMI Creation
* EC2 Image Management
* Application Pre-Configuration
* AMI Reusability
* Standardized EC2 Deployment
* Golden AMI Strategy

### Real-World Use Cases

* Standardized server deployment
* Faster infrastructure provisioning
* Application environment replication
* Auto Scaling
* Disaster Recovery

---

## 2. Secure Custom AMI Creation

### Objective

Created a reusable custom AMI after preparing and securing an EC2 instance.

The implementation included system updates, Apache installation, service configuration, cleanup of temporary files and history, and validation of the resulting AMI.

### Security Practices Implemented

* Updated operating system packages
* Key-based SSH authentication
* Configured security groups
* Removed unnecessary temporary data
* Avoided storing sensitive information in the image
* Validated the AMI before reuse

### Key Concepts

* Secure Image Creation
* Instance Hardening
* AMI Lifecycle Management
* Secure EC2 Deployment
* Reusable Infrastructure

---

## 3. AMI Copy Between AWS Regions

### Objective

Copied a custom AMI from **us-east-1 (N. Virginia)** to **ap-south-1 (Mumbai)** and used the copied AMI to launch an EC2 instance in the destination Region.

### Key Concepts

* Cross-Region AMI Replication
* EBS Snapshot Replication
* Multi-Region Deployment
* Disaster Recovery
* Regional Resilience

### Real-World Use Cases

* Disaster Recovery
* Regional Failure Protection
* Multi-Region Application Deployment
* Business Continuity
* Backup and Recovery Strategy

---

## 4. Auto Scaling with Custom AMI

### Objective

Integrated a custom AMI with an EC2 Launch Template and Auto Scaling Group to build automated, scalable, and self-healing infrastructure.

The Auto Scaling Group was configured with:

* Desired Capacity: 2
* Minimum Capacity: 2
* Maximum Capacity: 4
* Multiple Availability Zones

The environment was tested by terminating an EC2 instance and verifying that the Auto Scaling Group automatically launched a replacement instance.

### Key Concepts

* Custom AMI
* Launch Template
* Auto Scaling Group
* Multi-AZ Deployment
* Self-Healing Infrastructure
* Immutable Infrastructure
* Golden AMI Strategy
* Automated Deployment

---

# AMI Architecture

The projects in this module demonstrate the following progression:

```text
Configured EC2 Instance
        │
        ▼
   Custom AMI
        │
        ├───────────────► Launch New EC2 Instance
        │
        ├───────────────► Copy to Another AWS Region
        │
        │                  └──► Launch EC2 in Destination Region
        │
        └───────────────► Launch Template
                              │
                              ▼
                       Auto Scaling Group
                              │
                    ┌─────────┴─────────┐
                    ▼                   ▼
                 EC2 #1              EC2 #2
                    │                   │
                    └───────┬───────────┘
                            │
                       Self-Healing
```

---

# Skills Demonstrated

* AWS EC2
* Amazon Machine Images (AMI)
* EBS Snapshot Concepts
* Launch Templates
* Auto Scaling Groups
* Multi-AZ Architecture
* Cross-Region Deployment
* Disaster Recovery Concepts
* Infrastructure Standardization
* Secure Image Creation
* Linux Server Configuration
* Apache Web Server
* Cloud Infrastructure Automation

---

# Key Learnings

Through these projects, I developed a practical understanding of how AMIs are used to create consistent and repeatable EC2 deployments.

I learned how a properly configured EC2 instance can be converted into a reusable image and subsequently used to deploy identical environments without repeating the complete server configuration process.

I also gained practical experience in combining AMIs with other AWS capabilities such as Launch Templates and Auto Scaling Groups to create scalable and self-healing infrastructure.

The cross-region implementation further strengthened my understanding of how AMIs can support disaster recovery and multi-region deployment strategies.

---

# Real-World Applications

## Golden AMI Strategy

Organizations can maintain a standardized, pre-configured AMI containing:

* Approved operating system configuration
* Required applications
* Security updates
* Monitoring agents
* Organization-specific configurations

New EC2 instances can then be launched from this image instead of configuring each server manually.

---

## Auto Scaling

Custom AMIs can be integrated with Launch Templates and Auto Scaling Groups to automatically create identical EC2 instances when additional capacity is required.

This improves:

* Deployment consistency
* Scalability
* Availability
* Recovery time

---

## Disaster Recovery

AMI copies can be maintained in another AWS Region so that infrastructure can be recreated if the primary Region becomes unavailable.

This supports:

* Business continuity
* Regional disaster recovery
* Infrastructure replication
* Faster recovery

---

# Production Best Practices

* Keep AMIs updated with current security patches.
* Do not store passwords, private keys, API keys, or other secrets inside AMIs.
* Use IAM roles instead of hard-coded AWS credentials.
* Follow the Principle of Least Privilege.
* Remove unnecessary packages and temporary files before creating production AMIs.
* Use descriptive AMI names and versioning conventions.
* Maintain separate AMIs for different application environments when required.
* Test AMIs before using them in production Auto Scaling Groups.
* Regularly deprecate outdated AMIs.
* Store critical AMIs in secondary AWS Regions when required for disaster recovery.
* Use Launch Templates with version control when integrating AMIs with Auto Scaling.

---

# Repository Structure

```text
Amazon-Machine-Image-AMI/
│
├── README.md
│
├── Create-Custom-AMI-from-EC2-Instance/
│   ├── README.md
│   └── Screenshots/
│
├── Secure-Custom-AMI-Creation/
│   ├── README.md
│   └── Screenshots/
│
├── AMI-Copy-Between-Regions/
│   ├── README.md
│   └── Screenshots/
│
└── Auto-Scaling-with-Custom-AMI/
    ├── README.md
    └── Screenshots/
```

Each project contains its own detailed documentation and step-by-step implementation screenshots.

---

# Project Outcomes

After completing these practical implementations, I gained hands-on experience with the AMI lifecycle and its integration with other AWS services.

The projects helped me understand how organizations can move from manually configured EC2 servers toward standardized, reusable, scalable, and resilient cloud infrastructure.

The combination of **Custom AMIs, Launch Templates, Auto Scaling, Multi-AZ architecture, and Cross-Region replication** provided practical exposure to important cloud engineering concepts such as automation, high availability, disaster recovery, and self-healing infrastructure.

---

# Conclusion

These AMI projects demonstrate the practical use of Amazon Machine Images for building consistent and reusable AWS infrastructure.

Starting with a basic custom AMI and progressing toward secure image creation, cross-region replication, and Auto Scaling integration, this project series demonstrates how AMIs can become a foundation for scalable and production-oriented EC2 deployments.

This hands-on work strengthened my understanding of AWS compute infrastructure and how standardized machine images can be used to improve deployment speed, consistency, availability, and operational reliability.
