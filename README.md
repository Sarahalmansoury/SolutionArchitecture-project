# SolutionArchitecture-project

# Serverless Image Processing with S3, SQS, and Lambda

## Overview
This project aims to create a highly resilient, cost-optimized, and event-driven serverless image processing application. Users request a secure Pre-signed URL to upload images directly to an S3 source bucket. S3 then publishes event notifications to an SQS queue to decouple the process. A single, consolidated AWS Lambda function polls the queue and efficiently handles the entire processing workflow (validates, resizes, watermarks, and stores). Finally, the processed versions are stored in a destination S3 bucket and served globally via CloudFront.

The AWS services used in this project are:
- **Amazon S3**: For storing original and processed images, utilizing bucket policies and lifecycle rules.
- **Amazon SQS & DLQ**: To decouple events from processing and handle failures via a Dead-Letter Queue.
- **AWS Lambda**: A consolidated function for polling SQS and executing all image processing tasks to improve operational efficiency and reduce costs. It utilizes **Lambda Layers** for the Sharp library.
- **Amazon API Gateway**: To provide a Pre-signed URL generation endpoint for secure uploads.
- **Amazon DynamoDB**: For storing metadata about the images (upload time, dimensions, status).
- **Amazon CloudFront**: To serve processed images with low latency globally.
- **Amazon SNS**: To notify users on job completion or failure.
- **IAM**: For securing access to resources with fine-grained policies.

## Architecture Diagram
<img width="1066" height="498" alt="مشروع مناره drawio (1)" src="https://github.com/user-attachments/assets/92013dfa-22f7-47ea-ad65-310a845706a5" />


## Features
- Generate Pre-signed URLs via API Gateway for secure and direct S3 uploads.
- Decouple event generation from processing using SQS to improve resilience and handle traffic spikes.
- Trigger a single, consolidated AWS Lambda function to efficiently execute all processing tasks (validate → resize → watermark → store).
- Store processed images in a separate S3 bucket configured with lifecycle policies.
- Serve processed content globally with appropriate cache behaviors using CloudFront.
- Send automated notifications on job completion or failure via SNS.
- Secure access with IAM Roles.
- Store image metadata in DynamoDB.

## How to Deploy
1. Set up the original and processed S3 buckets, and configure lifecycle rules.
2. Create the SQS Main Queue and DLQ, and configure S3 to send event notifications to the queue.
3. Deploy the Lambda functions (the API Gateway URL generator and the consolidated SQS poller/processor) and package the Sharp library using Lambda Layers.
4. Configure the necessary IAM permissions for all services.
5. Set up DynamoDB, the SNS topic, and the CloudFront distribution.
6. Deploy the solution using AWS Console or AWS CLI.

## How to Use
- Request an upload URL via the API Gateway endpoint.
- Upload an image directly to the original S3 bucket using the provided Pre-signed URL.
- The system will asynchronously decouple the event via SQS, and a single Lambda function will process the image and save the final result to the destination bucket.
- Receive an SNS notification once the process succeeds or fails.
- Access the processed images globally with low latency from the CloudFront URL.

## Additional Notes
- The project uses the Sharp library packaged as a **Lambda Layer** for efficient image processing and smaller deployment sizes.
- The architecture is optimized for cost and operational efficiency by consolidating the image processing steps into a single Lambda function, avoiding the overhead of workflow orchestrators for this scale.
- Security is ensured through fine-grained IAM policies to prevent unauthorized access.
- The architecture is highly resilient; SQS decoupling prevents system overload during traffic spikes and enables retries via a Dead-Letter Queue.

---

**Project Author:** [sarahalmansouri]  
**Date Created:** [3/7/2026]
