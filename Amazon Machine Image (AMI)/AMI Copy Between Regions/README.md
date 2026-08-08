# AMI Copy Between AWS Regions

## Project Overview

This hands-on project demonstrates how to copy an Amazon Machine Image (AMI) from one AWS Region to another and use the copied AMI to launch an EC2 instance in the destination Region.

The purpose of this implementation was to understand how AMIs can be replicated across AWS Regions to support **disaster recovery, business continuity, regional deployment, and infrastructure replication**.

In this lab, a custom AMI created in the source Region was copied to the destination Region. The copied AMI was then used to launch a new EC2 instance, and the deployed environment was validated to ensure that the application and server configuration were successfully replicated.

---

# Project Objective

The objective of this project was to gain practical experience with **cross-region AMI replication** and understand how organizations can use AMIs to recreate standardized EC2 infrastructure in another AWS Region.

This implementation helped me understand the relationship between AMIs and EBS snapshots, the process of copying images across Regions, and how replicated AMIs can be used as part of a disaster recovery strategy.

---

# Lab Environment

| Component          | Configuration             |
| ------------------ | ------------------------- |
| Cloud Provider     | AWS                       |
| Source Region      | `us-east-1` (N. Virginia) |
| Destination Region | `ap-south-1` (Mumbai)     |
| Compute Service    | Amazon EC2                |
| Image Type         | Custom AMI                |
| Storage            | Amazon EBS                |
| Access Method      | AWS Management Console    |

---

# Architecture

```text
                 SOURCE AWS REGION
                  us-east-1
                      │
                      ▼
              ┌───────────────┐
              │  Custom AMI   │
              │   (Source)    │
              └───────┬───────┘
                      │
                      │ Copy AMI
                      ▼
              ┌───────────────┐
              │ AWS AMI Copy  │
              │    Process    │
              └───────┬───────┘
                      │
                      ▼
              DESTINATION REGION
                  ap-south-1
                      │
                      ▼
              ┌───────────────┐
              │  Copied AMI   │
              └───────┬───────┘
                      │
                      ▼
              ┌───────────────┐
              │ New EC2       │
              │ Instance      │
              └───────┬───────┘
                      │
                      ▼
              Replicated Application
              & Server Configuration
```

---

# Why Copy AMIs Between Regions?

An AMI is Region-specific. A custom AMI created in one AWS Region cannot directly be used to launch an EC2 instance in another Region.

Copying the AMI allows the image to be replicated into another Region.

This is useful for:

* Disaster Recovery
* Business Continuity
* Multi-Region Deployment
* Regional Application Deployment
* Infrastructure Replication
* Faster Recovery from Regional Failures

---

# Implementation Workflow

## Step 1 – Identify the Source AMI

Logged into the AWS Management Console and navigated to the Amazon EC2 service.

Located the custom AMI available in the source Region:

```text
Source Region: us-east-1
```

The AMI contained the required operating system and application configuration.

[Step 1](Screenshots/step-01.png) - to - [Step 7](Screenshots/step-07.png)

---

## Step 2 – Review AMI Configuration

Reviewed the selected AMI before initiating the copy operation.

Verified:

* AMI Name
* AMI ID
* Architecture
* Root Device Type
* EBS Snapshot
* AMI State

[Step 8](Screenshots/step-08.png)

---

## Step 3 – Initiate AMI Copy

Selected the custom AMI and initiated the **Copy AMI** operation.

Specified the destination Region:

```text
Destination Region: ap-south-1
```

[Step 8](Screenshots/step-08.png) - tp - [Step 3](Screenshots/step-11.png)

---

## Step 4 – Configure Destination AMI

Configured the destination AMI name and initiated the copy process.

The AMI copy operation creates a new AMI in the destination Region based on the source image.

[Step 12](Screenshots/step-12.png) - to - [Step 16](Screenshots/step-16.png)

---

## Step 5 – Monitor AMI Copy

Switched to the destination AWS Region and monitored the AMI copy operation.

The copied AMI initially appeared in a pending state while AWS replicated the underlying image data.

---

## Step 6 – Verify AMI Availability

Waited for the AMI copy operation to complete.

Verified that the destination AMI reached the:

```text
Available
```

state.

---

## Step 7 – Launch EC2 Instance from Copied AMI

Used the copied AMI to launch a new EC2 instance in the destination Region.

Configured the required:

* Instance Type
* Key Pair
* Network
* Subnet
* Security Group
* Storage
  
---

## Step 8 – Verify EC2 Instance

Verified that the newly launched EC2 instance was running successfully in the destination Region.

Confirmed that the instance was created using the copied AMI.

---

## Step 9 – Validate Replicated Configuration

Connected to the newly launched EC2 instance and verified that the expected operating system and application configuration were available.

The objective was to confirm that the copied AMI successfully preserved the required server environment.

[Step 17](Screenshots/step-17.png) - to - [Step 18](Screenshots/step-18.png)

---

# Validation

The implementation was considered successful after verifying:

* Source AMI was available in `us-east-1`.
* AMI copy operation completed successfully.
* Destination AMI became available in `ap-south-1`.
* EC2 instance was successfully launched using the copied AMI.
* Expected operating system configuration was available.
* Application/server configuration was successfully replicated.
* Destination infrastructure operated independently in the new Region.

---

# AMI and EBS Relationship

When an EBS-backed AMI is copied to another Region, AWS also creates copies of the underlying EBS snapshots required by the AMI.

Conceptually:

```text
Source Region

EC2 Instance
     │
     ▼
   AMI
     │
     ▼
EBS Snapshot
     │
     │  Copy
     ▼
Destination Region
     │
     ▼
Copied EBS Snapshot
     │
     ▼
Copied AMI
     │
     ▼
New EC2 Instance
```

This allows the destination AMI to be used independently within the destination Region.

---

# Disaster Recovery Use Case

Consider an application running in:

```text
Primary Region
us-east-1
```

A business may maintain a replicated AMI in:

```text
DR Region
ap-south-1
```

If the primary Region becomes unavailable, the organization can use the replicated AMI to recreate EC2 infrastructure in the DR Region.

Example:

```text
             Production
              us-east-1
                  │
                  │
              Custom AMI
                  │
                  │ Replication
                  ▼
              ap-south-1
                  │
                  ▼
          DR EC2 Infrastructure
```

This approach can help reduce recovery time and support business continuity.

---

# Security Considerations

The following security considerations were followed during the implementation:

* Avoided storing passwords or sensitive credentials inside the AMI.
* Used IAM permissions appropriate for AMI management.
* Used secure EC2 Security Group rules.
* Used SSH key-based authentication where applicable.
* Ensured that the destination AMI was available before launching infrastructure.
* Verified the replicated environment after deployment.

---

# Production Best Practices

* Maintain AMIs with a clear versioning and naming convention.
* Regularly update AMIs with security patches.
* Remove sensitive information before creating production images.
* Maintain critical AMIs in a secondary Region for disaster recovery.
* Test replicated AMIs periodically rather than assuming they will work during an actual disaster.
* Control AMI sharing and permissions carefully.
* Monitor AMI and snapshot usage to manage storage costs.
* Document the Region, AMI version, application version, and creation date.
* Combine cross-region AMI replication with automated infrastructure provisioning where possible.

---

# Key Learnings

Through this project, I gained practical experience in:

* Understanding Region-specific AMI availability.
* Copying AMIs between AWS Regions.
* Understanding the relationship between AMIs and EBS snapshots.
* Launching EC2 instances from replicated AMIs.
* Implementing basic cross-region infrastructure replication.
* Understanding AMI-based disaster recovery.
* Validating replicated infrastructure after deployment.

---

# Skills Demonstrated

* Amazon EC2
* Amazon Machine Images (AMI)
* Amazon EBS
* Cross-Region Infrastructure
* Disaster Recovery Concepts
* Business Continuity
* Cloud Infrastructure Replication
* AWS Management Console
* EC2 Deployment
* Cloud Security Best Practices

---

# Project Outcome

Successfully replicated a custom Amazon Machine Image from `us-east-1` to `ap-south-1` and used the replicated image to launch a new EC2 instance.

The project demonstrated how AMIs can be used to maintain consistent server configurations across AWS Regions and form an important component of a disaster recovery and business continuity strategy.

This implementation strengthened my understanding of **multi-region cloud infrastructure, EC2 image management, and disaster recovery concepts** relevant to Cloud Engineering.

---

# Screenshots

The `Screenshots/` directory contains the step-by-step implementation evidence for this project, including:

* Source AMI Selection
* AMI Configuration
* Copy AMI Operation
* Destination Region Selection
* AMI Copy Progress
* Destination AMI Verification
* EC2 Launch from Copied AMI
* Instance Verification
* Application/Server Validation

Each screenshot documents a specific stage of the implementation and provides practical evidence of the completed cross-region AMI deployment.
