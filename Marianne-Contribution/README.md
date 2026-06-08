# Marianne’s Contribution – IT 261 Final Project  
**Personal GitHub:** https://github.com/MarianneCrow5

---

# AWS Terraform Pipeline – Final Project

This project demonstrates a complete AWS infrastructure deployment using Terraform, including IAM, Lambda, S3, and ECS components. It represents my individual contribution to the group’s serverless image‑processing pipeline.

---

## 🚀 Project Overview

This repository contains my portion of the IT 261 final project, which includes:

- Terraform configuration files (IAM, Lambda, S3, ECS, variables, etc.)
- Lambda function code
- Documentation files
- Architecture diagrams
- Required screenshots demonstrating the working pipeline
- Statement of Work and project checklist

The project provisions AWS resources using Terraform, deploys a Lambda function, and demonstrates automated infrastructure deployment.

---

## 🧩 Presigned URL Generator (Lightweight Lambda)

To support uploading any user‑selected image to the S3 input bucket, the project includes a small Lambda function that generates pre‑signed S3 URLs on demand.

This Lambda:

- Runs only when a user uploads a file  
- Executes for a few milliseconds  
- Has negligible cost  
- Does not affect the previously submitted project budget  

It enables the upload page to:

- Request a fresh pre‑signed URL for each file  
- Support any filename and content type  
- Securely upload images to the S3 input bucket  

This is a standard component of S3 upload architecture and ensures the frontend upload tool works reliably.

---

## 🖼️ S3‑Triggered Lambda: Image Metadata Processor

This Lambda function is the entry point for my portion of the serverless pipeline. It is triggered automatically whenever a new file is uploaded to the designated S3 input bucket.

### Trigger
- Event Source: s3:ObjectCreated:*  
- Bucket: Shared input bucket (ARN provided in Terraform variables)

### Function Responsibilities
- Parse S3 event notification to extract:
  - Bucket name  
  - Object key  
  - Timestamp  
  - File size  
  - File type  
- Validate uploaded object (image file, non‑zero size)  
- Generate a unique record ID  
- Write a structured item to the shared DynamoDB table (bmr-dynamodb-table) including:
  - id (UUID)  
  - filename  
  - bucket  
  - timestamp  
  - filesize  
  - filetype  
  - status (“received”)  
  - notes (“Initial metadata recorded”)

### Outputs
- A DynamoDB record representing the uploaded file  
- CloudWatch logs for debugging and traceability  

### Why This Matters
This Lambda establishes the first step in the pipeline and ensures every uploaded file is tracked consistently. It decouples the upload interface from downstream processing, allowing the ECS/Fargate stage to operate independently.

---

## 🛠️ Terraform File Overview

- main.tf – AWS provider and region  
- variables.tf – Input variables  
- S3.tf – Input/output S3 buckets  
- iam.tf – IAM roles and policies  
- lambda.tf – Lambda deployment and permissions  
- ecs.tf – ECS task definition for downstream processing  

---

## ▶️ How to Run the Project

1. Install Terraform  
2. Configure AWS credentials  
3. Run terraform init  
4. Run terraform apply  

---

## 📁 Repository Structure

- /terraform – All Terraform configuration files  
- /Documentation – Final Turn In doc, SOW, required screenshots, and diagrams  
- /Interface – Upload interface files  
- /Diagrams – Architecture diagrams  
- /screenshots – (If used) supporting images  

---

## 🖼️ Screenshots

All required screenshots and diagrams are included in the Final Turn In documentation file located in the Documentation folder.

---
