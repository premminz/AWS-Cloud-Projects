# Highly Available Web Application using ELB + Auto Scaling Group

## Project Overview

This hands-on AWS project demonstrates the deployment of a **highly available, scalable, and self-healing web application** using an Application Load Balancer (ALB) and an EC2 Auto Scaling Group (ASG).

The architecture is designed so that incoming application traffic is distributed across multiple EC2 instances while the Auto Scaling Group continuously maintains the required number of healthy instances.

As part of this implementation, I configured an EC2 Launch Template, deployed instances across multiple Availability Zones, created an Application Load Balancer and Target Group, configured health checks, and validated the self-healing behavior by terminating an EC2 instance and observing the automatic replacement process.

---

# Project Objective

The objective of this project was to understand how **Elastic Load Balancing and EC2 Auto Scaling work together to provide high availability, scalability, and fault tolerance**.

Through this hands-on implementation, I gained practical experience in designing an AWS architecture where application traffic is automatically distributed across healthy instances and failed instances are automatically replaced without manual intervention.

---

# Business Scenario

Consider a web application that must remain available even if one of its backend servers fails.

A traditional single-server architecture creates a **Single Point of Failure (SPOF)**:

```text
                 Users
                   │
                   ▼
              EC2 Server
                   │
                   X
                Failure
                   │
                   ▼
             Application Down
```

To eliminate this dependency, the application can be deployed using multiple EC2 instances behind an Application Load Balancer and managed by an Auto Scaling Group.

```text
                         Users
                           │
                           ▼
                 Application Load Balancer
                           │
                 ┌─────────┴─────────┐
                 ▼                   ▼
             EC2 Instance        EC2 Instance
                 │                   │
              AZ-1                AZ-2
                 │                   │
                 └─────────┬─────────┘
                           │
                    Auto Scaling Group
```

If one instance fails, the Auto Scaling Group automatically launches a replacement.

---

# Architecture

```text
                         Internet
                            │
                            ▼
                 ┌─────────────────────┐
                 │ Application Load    │
                 │ Balancer (ALB)       │
                 └──────────┬──────────┘
                            │
                     Target Group
                            │
              ┌─────────────┴─────────────┐
              │                           │
              ▼                           ▼
       Availability Zone A          Availability Zone B
              │                           │
         ┌─────────┐                 ┌─────────┐
         │ EC2 #1  │                 │ EC2 #2  │
         │ Web App │                 │ Web App │
         └─────────┘                 └─────────┘
              │                           │
              └─────────────┬─────────────┘
                            │
                   Auto Scaling Group
                            │
                   Desired: 2 Instances
                   Minimum: 2 Instances
                   Maximum: 4 Instances
```

---

# AWS Services Used

* Amazon EC2
* Application Load Balancer (ALB)
* EC2 Auto Scaling Group
* Launch Template
* Target Groups
* Amazon VPC
* Security Groups
* Availability Zones
* Amazon CloudWatch

---

# Configuration

| Component              | Configuration               |
| ---------------------- | --------------------------- |
| Load Balancer          | Application Load Balancer   |
| Load Balancer Scheme   | Internet-facing             |
| Target Type            | Instances                   |
| Minimum Capacity       | 2                           |
| Desired Capacity       | 2                           |
| Maximum Capacity       | 4                           |
| Deployment             | Multiple Availability Zones |
| Backend                | Amazon EC2                  |
| Health Monitoring      | Target Group Health Checks  |
| Instance Configuration | Launch Template             |

---

# Implementation Workflow

## Step 1 – Prepare the Web Server Configuration

Prepared the web server environment that would be used by the EC2 instances.

The required application/web server configuration was installed and tested before creating the reusable Launch Template.

---

## Step 2 – Create an EC2 Launch Template

Created an EC2 Launch Template containing the configuration required for instances launched by the Auto Scaling Group.

The Launch Template defined parameters such as:

* AMI
* Instance Type
* Key Pair
* Security Group
* Storage
* User Data / Web Server Configuration

This ensures that every instance launched by the Auto Scaling Group follows the same configuration.

---

## Step 3 – Create a Target Group

Created a Target Group for the backend EC2 instances.

Configured:

* Target Type
* Protocol
* Port
* Health Check
* Health Check Path

The Target Group provides the connection between the Application Load Balancer and backend EC2 instances.

---

## Step 4 – Configure Health Checks

Configured health checks to determine whether backend EC2 instances were available to serve application traffic.

The ALB uses the Target Group health status to route requests only toward healthy targets.

---

## Step 5 – Create an Application Load Balancer

Created an internet-facing Application Load Balancer to act as the single entry point for users.

Configured:

* Load Balancer Name
* Scheme
* Availability Zones
* Security Group
* Listener
* Target Group

---

## Step 6 – Create the Auto Scaling Group

Created an Auto Scaling Group using the previously created Launch Template.

Configured the capacity:

```text
Minimum Capacity: 2
Desired Capacity: 2
Maximum Capacity: 4
```

The Auto Scaling Group was configured across multiple Availability Zones to improve application availability.

---

## Step 7 – Configure Load Balancer Integration

Associated the Auto Scaling Group with the Application Load Balancer Target Group.

This allowed newly launched instances to automatically become part of the load-balanced application environment.

---

## Step 8 – Verify EC2 Instances

Verified that the Auto Scaling Group automatically launched the required number of EC2 instances.

Expected state:

```text
Desired: 2
Minimum: 2
Maximum: 4
```

Both instances were registered with the Target Group.

---

## Step 9 – Verify Target Health

Checked the Target Group and confirmed that the EC2 instances were passing their health checks.

Expected result:

```text
EC2 #1 → Healthy
EC2 #2 → Healthy
```

---

## Step 10 – Test Application through ALB

Accessed the application using the DNS name of the Application Load Balancer.

The ALB successfully accepted incoming requests and forwarded them to healthy backend instances.

---

# High Availability Validation

The architecture was tested to confirm that the application remained available even when an individual backend instance became unavailable.

The validation process included:

1. Confirming multiple EC2 instances were running.
2. Confirming both instances were healthy.
3. Accessing the application through the ALB.
4. Terminating one EC2 instance manually.
5. Monitoring the Auto Scaling Group.
6. Confirming that ASG detected the capacity reduction.
7. Verifying that a replacement EC2 instance was automatically launched.
8. Confirming that the replacement instance became healthy.
9. Validating application availability through the ALB.

---

# Self-Healing Demonstration

One of the most important objectives of this project was to demonstrate **self-healing infrastructure**.

Before failure:

```text
Desired Capacity = 2

EC2 #1 → Healthy
EC2 #2 → Healthy
```

After manually terminating one instance:

```text
EC2 #1 → Terminated
EC2 #2 → Healthy
```

Auto Scaling Group detects that the number of running instances has fallen below the desired capacity.

```text
Desired Capacity = 2
Current Capacity = 1

        ↓

ASG launches replacement instance

        ↓

New EC2 Instance → Target Group

        ↓

Health Check

        ↓

Healthy
```

Final state:

```text
EC2 #2 → Healthy
EC2 #3 → Healthy
```

The application continues to be served through the Application Load Balancer.

This demonstrates the **self-healing capability** of the architecture.

---

# Traffic Flow

The complete request flow is:

```text
Client
  │
  │ HTTP Request
  ▼
Application Load Balancer
  │
  ▼
Target Group
  │
  ├──────────────► EC2 Instance 1
  │
  └──────────────► EC2 Instance 2
                         │
                         ▼
                    Web Application
```

The ALB continuously evaluates target health and avoids routing traffic to unhealthy targets.

---

# Fault Tolerance

The architecture removes the dependency on a single EC2 instance.

If one instance becomes unavailable:

```text
Before Failure

ALB
 │
 ├── EC2 #1 ✓
 └── EC2 #2 ✓


Instance #1 Failure

ALB
 │
 └── EC2 #2 ✓


Auto Scaling

ASG → Launch Replacement


After Recovery

ALB
 │
 ├── EC2 #2 ✓
 └── EC2 #3 ✓
```

This improves application resilience and reduces downtime caused by individual instance failures.

---

# Security Considerations

The following security considerations were applied during the implementation:

* Configured Security Groups according to required traffic flows.
* Allowed application traffic through the Load Balancer.
* Restricted backend access where applicable.
* Used IAM permissions according to required responsibilities.
* Avoided exposing unnecessary services and ports.
* Used health checks to prevent traffic from being sent to unhealthy instances.

---

# Key Learnings

Through this project, I gained hands-on experience with:

* Application Load Balancer
* Auto Scaling Groups
* Launch Templates
* Target Groups
* EC2 Health Checks
* Multi-AZ Architecture
* Traffic Distribution
* Fault Tolerance
* Self-Healing Infrastructure
* Scalable Application Architecture

Most importantly, I learned how **ELB and Auto Scaling complement each other**:

```text
ELB
 ↓
Distributes Traffic
 ↓
Healthy EC2 Instances


Auto Scaling
 ↓
Maintains Capacity
 ↓
Replaces Failed Instances
```

Together, they provide a highly available and resilient application architecture.

---

# Skills Demonstrated

* AWS Cloud Infrastructure
* Amazon EC2
* Application Load Balancer
* Auto Scaling Groups
* Launch Templates
* Target Groups
* Health Checks
* High Availability
* Fault Tolerance
* Self-Healing Infrastructure
* Multi-AZ Deployment
* Cloud Networking
* AWS Security

---

# Production Best Practices

For a production environment, this architecture can be further improved by:

* Deploying resources across multiple Availability Zones.
* Using HTTPS listeners with AWS Certificate Manager.
* Keeping backend EC2 instances in private subnets.
* Using Auto Scaling policies based on CPU utilization or application metrics.
* Integrating CloudWatch for monitoring and alerting.
* Using IAM Roles instead of hard-coded credentials.
* Enabling ALB access logging.
* Implementing centralized logging and monitoring.
* Using Infrastructure as Code such as Terraform or AWS CloudFormation.
* Maintaining versioned Launch Templates and AMIs.

---

# Project Outcome

Successfully deployed a highly available web application architecture using **Application Load Balancer, EC2 Auto Scaling Group, Launch Template, Target Group, and multiple Availability Zones**.

The implementation successfully demonstrated:

* Load balancing across multiple EC2 instances
* Health-based traffic routing
* Automatic instance provisioning
* Automatic replacement of failed instances
* High availability across Availability Zones
* Self-healing infrastructure

The failure simulation confirmed that the application infrastructure could automatically recover from an EC2 instance failure without requiring manual instance creation.

This project strengthened my practical understanding of designing **scalable, fault-tolerant, and highly available AWS infrastructure**.

---
