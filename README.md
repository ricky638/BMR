# 📷 Serverless Event-Driven Image Properties Processing Pipeline

Welcome to our group project repository. This project outlines a public blueprint for a serverless, event-driven image processing and metadata extraction pipeline built natively on AWS.

Anyone is welcome to copy, fork, or adapt this architecture format for their own use cases.

## 📁 Repository Layout

```text
├── docs/
│   └── pipeline_manifest.json    # Structural technical format of the pipeline (JSON)
└── README.md                     # System overview and machine setup instructions (This file)
```

## 🏗️ Architecture Design & Project Services

Our system utilizes an event-driven flow to process images instantly upon upload without keeping servers running 24/7.

*   **Amazon S3**: Ingestion bucket where user uploads raw images.
*   **AWS Lambda**: Serverless event processor triggered automatically by S3.
*   **Amazon ECR**: Hosts container images used for heavy image manipulation tasks.
*   **AWS Fargate**: Serverless container compute that executes image manipulation tasks pulled from ECR.
*   **Amazon Rekognition**: Computer vision API that analyzes the image and returns descriptive tags.
*   **Amazon DynamoDB**: NoSQL database storing the final image properties and extracted metadata.

---

## 🔄 Technical Pipeline Steps

The end-to-end workflow of the machine follows these sequential phases:
1. **User Uploads Image to S3**: The pipeline begins when an image is placed into the designated bucket.
2. **S3 Event Notification**: S3 publishes a real-time event notice immediately upon file creation.
3. **Lambda Triggered**: AWS Lambda consumes the S3 event and reads the file details.
4. **Image Manipulation & AI Tagging**: Lambda routes processing tasks to Fargate (via ECR) for modifications and interfaces with Amazon Rekognition to pull semantic object tags.
5. **Database Entry**: Extracted metadata and properties are structured and written to Amazon DynamoDB.

---

## 📑 How to Read and Utilize the JSON Blueprint

We have provided a structural documentation-as-code file located at `docs/pipeline_manifest.json`. This file gives public users a clean, machine-readable breakdown of the services and architecture pipeline steps.

### Viewing the Layout Locally
To examine the technical structural blueprint on your own machine:
1. Clone or copy this repository to your local computer:
   ```bash
   git clone <YOUR_GITHUB_REPOSITORY_URL>
   ```
2. Navigate to the documentation directory:
   ```bash
   cd docs
   ```
3. Open `pipeline_manifest.json` using your favorite text editor, IDE, or web browser to review the pipeline mapping schemas.

## Team BMR Members
**b** Beau
**M** Marianne
**R** Ricky
