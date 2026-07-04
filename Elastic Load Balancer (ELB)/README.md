# Elastic Load Balancer (ELB)

## Overview

This repository contains my hands-on AWS Elastic Load Balancer (ELB) projects completed as part of my Cloud Engineering learning journey.

The objective of this module is to understand how AWS distributes incoming traffic across multiple Amazon EC2 instances to improve application availability, scalability, fault tolerance, and overall performance.

Each project demonstrates a real-world implementation of load balancing and high availability using different AWS services and architectures.

---

# Learning Objectives

Through these practical labs, I gained hands-on experience in:

* Understanding the architecture of AWS Elastic Load Balancer (ELB)
* Configuring Application Load Balancers (ALB)
* Creating and managing Target Groups
* Registering Amazon EC2 instances
* Configuring Health Checks
* Implementing High Availability architectures
* Deploying Auto Scaling Groups (ASG)
* Securing applications using HTTPS
* Configuring SSL/TLS certificates
* Validating traffic distribution across multiple EC2 instances
* Building scalable and production-ready cloud infrastructure

---

# AWS Services Used

* Amazon EC2
* Elastic Load Balancer (ELB)
* Application Load Balancer (ALB)
* Auto Scaling Group (ASG)
* Target Groups
* Amazon VPC
* Security Groups
* Amazon Certificate Manager (ACM)
* Route 53 (where applicable)

---

# Projects Included

## 1. EC2 Load Balancing using Application Load Balancer

**Objective**

Deploy multiple EC2 instances behind an Application Load Balancer to distribute incoming HTTP requests efficiently.

**Key Concepts**

* Application Load Balancer
* Target Groups
* Health Checks
* Traffic Distribution
* High Availability

---

## 2. Highly Available Web Application using ELB + Auto Scaling Group

**Objective**

Build a highly available web application capable of automatically replacing unhealthy instances and scaling based on workload.

**Key Concepts**

* Auto Scaling Group
* Application Load Balancer
* Launch Template
* Multi-AZ Deployment
* Automatic Instance Replacement

---

## 3. HTTPS Load Balancer with Auto Scaling

**Objective**

Secure a web application using HTTPS while combining Auto Scaling and Application Load Balancer for improved security and availability.

**Key Concepts**

* HTTPS Listener
* SSL/TLS Certificate
* AWS Certificate Manager (ACM)
* Secure Traffic
* Automatic Scaling
* High Availability

---

# Skills Demonstrated

* AWS Cloud Infrastructure
* Elastic Load Balancer (ELB)
* Application Load Balancer (ALB)
* High Availability Architecture
* Auto Scaling
* Fault Tolerance
* Traffic Distribution
* Health Check Configuration
* Secure Web Application Deployment
* Cloud Networking
* AWS Security Best Practices
* Infrastructure Documentation

---

# Key Learnings

By completing these projects, I developed practical experience in designing scalable and resilient cloud architectures capable of handling production workloads.

These implementations strengthened my understanding of how AWS Load Balancers interact with EC2 instances, Auto Scaling Groups, Target Groups, and networking components to ensure high availability, improved performance, and secure application delivery.

---

# Production Best Practices

* Deploy load balancers across multiple Availability Zones.
* Configure Health Checks for automatic failure detection.
* Use Target Groups to simplify backend management.
* Enable HTTPS using AWS Certificate Manager (ACM).
* Integrate ELB with Auto Scaling Groups.
* Apply the Principle of Least Privilege for IAM permissions.
* Monitor load balancer metrics using Amazon CloudWatch.
* Enable access logging for auditing and troubleshooting.

---

# About This Repository

Each project folder contains:

* A detailed project README
* Step-by-step implementation guide
* Architecture overview
* Configuration details
* Practical validation
* Screenshots captured during the implementation

These projects collectively demonstrate my hands-on experience with designing, deploying, and securing highly available applications on AWS using Elastic Load Balancer services.
