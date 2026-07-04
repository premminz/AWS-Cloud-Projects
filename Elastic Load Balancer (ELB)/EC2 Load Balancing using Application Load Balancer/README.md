# EC2 Load Balancing using Application Load Balancer (ALB)

## Project Overview

This project demonstrates the deployment of a highly available web application using an AWS Application Load Balancer (ALB) to distribute incoming HTTP traffic across multiple Amazon EC2 instances.

The implementation showcases how Application Load Balancer improves application availability, fault tolerance, scalability, and performance by routing client requests only to healthy backend servers.

This hands-on lab follows AWS best practices for deploying web applications in a production-like environment.

---

# Project Objective

The objective of this project was to understand the architecture and implementation of AWS Application Load Balancer (ALB) by configuring multiple EC2 instances behind a single load balancer.

Through this implementation, I gained practical experience in traffic distribution, target groups, health checks, security group configuration, and validating load balancing behavior across multiple web servers.

---

# Lab Environment

* Cloud Provider: AWS
* Compute Service: Amazon EC2
* Load Balancer: Application Load Balancer (ALB)
* Protocol: HTTP
* Target Type: Instance
* VPC: Default / Custom
* Security Groups
* Target Groups

---

# Architecture Overview

```text
                    Internet
                        │
                        ▼
        Application Load Balancer (ALB)
                        │
        ┌───────────────┴───────────────┐
        ▼                               ▼
    EC2 Instance 1                 EC2 Instance 2
        │                               │
      Apache/Nginx                   Apache/Nginx
```

The Application Load Balancer acts as a single entry point for client requests and distributes traffic across healthy EC2 instances.

---

# AWS Services Used

* Amazon EC2
* Elastic Load Balancer (Application Load Balancer)
* Target Groups
* Amazon VPC
* Security Groups
* EC2 Security Groups

---

# Project Workflow

### Step 1 – Launch Amazon EC2 Instances

Provisioned multiple EC2 instances to host the web application.

[Step 1](Screenshots/step%201.png)

---

### Step 2 – Configure Security Groups

Configured inbound rules to allow HTTP traffic and secure communication between resources.

[Step 4](Screenshots/step%204.png)

---

### Step 3 – Install and Configure Web Server

Installed and configured a web server on each EC2 instance.

Configured individual web pages to identify which server processed each request.

[Step 5](Screenshots/step%205.png) and [Step 9](Screenshots/step%209.png)

---

### Step 4 – Verify Web Server Accessibility

Validated that each EC2 instance was accessible independently before implementing load balancing.

---

### Step 5 – Create Target Group

Created a Target Group and registered the EC2 instances.

Configured health check settings to monitor backend server availability.

[Step 10](Screenshots/step-10.png) - to - [Step 18](Screenshots/step-18.png)

---

### Step 6 – Create Application Load Balancer

Configured an internet-facing Application Load Balancer.

Configured:

* Listener
* Availability Zones
* Security Group
* Target Group Association

[Step 19](Screenshots/step-19.png) - to - [Step 31](Screenshots/step-31.png)

---

### Step 7 – Register EC2 Instances

Associated both EC2 instances with the configured Target Group.

Verified successful registration.

---

### Step 8 – Configure Health Checks

Validated that the ALB health checks successfully identified healthy backend instances.

---

### Step 9 – Test Traffic Distribution

Accessed the ALB DNS Name using a web browser.

Verified that incoming requests were distributed across multiple EC2 instances.

[Step 32](Screenshots/step-32.png) - to - [Step 35](Screenshots/step-35.png)

---

### Step 10 – Validate Load Balancer Functionality

Performed multiple refresh operations and confirmed that requests were served alternately by different backend servers.

Verified successful load balancing behavior.

---

# Load Balancing Verification

The deployment was validated by confirming:

* Both EC2 instances were healthy.
* Target Group health checks passed.
* ALB successfully routed client requests.
* Multiple page refreshes reached different backend instances.
* The application remained available through the ALB endpoint.

---

# Security Best Practices Implemented

During this implementation, the following AWS best practices were applied:

* Used an Application Load Balancer instead of exposing individual instances.
* Configured Security Groups to allow only required traffic.
* Enabled Health Checks for automatic monitoring.
* Used Target Groups to simplify backend management.
* Deployed multiple backend servers for improved availability.
* Followed AWS networking best practices.

---

# Skills Demonstrated

* Amazon EC2
* Application Load Balancer (ALB)
* Target Groups
* Health Check Configuration
* Security Groups
* HTTP Load Balancing
* High Availability Architecture
* Traffic Distribution
* AWS Networking
* Cloud Infrastructure Deployment
* AWS Management Console

---

# Key Learnings

Through this project, I gained practical experience in:

* Deploying multiple EC2 web servers.
* Configuring an Application Load Balancer.
* Creating and managing Target Groups.
* Registering backend instances.
* Configuring Health Checks.
* Understanding Layer 7 (HTTP/HTTPS) load balancing.
* Verifying request distribution across multiple servers.
* Building scalable and highly available cloud applications.

---

# Project Outcome

This project successfully demonstrates how an AWS Application Load Balancer distributes incoming client requests across multiple EC2 instances while continuously monitoring backend health.

The implementation improved application availability, fault tolerance, and scalability by eliminating dependence on a single server. It also reflects how production environments use Application Load Balancers to deliver reliable and highly available web applications.

---

# Production Best Practices

* Deploy Application Load Balancers across multiple Availability Zones.
* Configure Health Checks for every Target Group.
* Restrict inbound traffic using Security Groups.
* Keep backend instances in private subnets whenever possible.
* Enable HTTPS using AWS Certificate Manager (ACM).
* Integrate ALB with Auto Scaling Groups.
* Monitor ALB metrics using Amazon CloudWatch.
* Enable access logs for troubleshooting and auditing.

---

# Screenshots

The **Screenshots** directory contains the complete implementation workflow, including:

* EC2 Instance Deployment
* Web Server Configuration
* Security Group Configuration
* Target Group Creation
* Application Load Balancer Creation
* Listener Configuration
* Instance Registration
* Health Check Validation
* Load Balancer DNS Testing
* Traffic Distribution Verification

Each screenshot corresponds to a practical implementation step and documents the successful deployment of an Application Load Balancer with multiple backend EC2 instances.
