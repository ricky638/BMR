# Marianne Crow – IT 261 Final Project  
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

This Lambda function is the entry point for my portion of the serverless pipeline. It is triggered automatically whenever a new file is uploaded to the designated S3 input bucket. The event source is the `s3:ObjectCreated:*` notification, which fires each time an object is created in the shared input bucket. The bucket ARN is provided through Terraform variables, ensuring the function is tightly integrated with the group’s shared infrastructure.

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
