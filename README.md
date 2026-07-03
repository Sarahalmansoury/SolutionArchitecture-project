# SolutionArchitecture-project

# Serverless Image Processing with S3, SQS, and Lambda

## Overview
This project aims to create a highly resilient, event-driven serverless image processing application. Users request a secure Pre-signed URL to upload images directly to an S3 source bucket. S3 then publishes event notifications to an SQS queue to decouple the process. A polling AWS Lambda function is automatically triggered to initiate AWS Step Functions, which coordinate a multi-step workflow (validate, resize, watermark, and store). Finally, the processed versions are stored in a destination S3 bucket and served globally via CloudFront.

The AWS services used in this project are:
- **Amazon S3**: For storing original and processed images, utilizing bucket policies and lifecycle rules.
- **Amazon SQS & DLQ**: To decouple events from processing and handle failures via a Dead-Letter Queue.
- **AWS Lambda**: For automatic image processing, utilizing **Lambda Layers** for the Sharp library.
- **AWS Step Functions**: To orchestrate the standard image processing workflow.
- **Amazon API Gateway**: To provide a Pre-signed URL generation endpoint for secure uploads.
- **Amazon DynamoDB**: For storing metadata about the images (upload time, dimensions, status).
- **Amazon CloudFront**: To serve processed images with low latency globally.
- **Amazon SNS**: To notify users on job completion or failure.
- **IAM**: For securing access to resources with fine-grained policies.

## Architecture Diagram
<img width="1436" height="517" alt="مشروع مناره drawio" src="https://github.com/user-attachments/assets/800482bb-13b9-4fca-af2c-9b2961443952" />


## Features
- Generate Pre-signed URLs via API Gateway for secure and direct S3 uploads.
- Decouple event generation from processing using SQS to improve resilience.
- Trigger AWS Lambda to process images through a Step Functions standard workflow (validate → resize → watermark → store).
- Store processed images in a separate S3 bucket configured with lifecycle policies.
- Serve processed content globally with appropriate cache behaviors using CloudFront.
- Send automated notifications on job completion or failure via SNS.
- Secure access with IAM Roles.
- Store image metadata in DynamoDB.

## How to Deploy
1. Set up the original and processed S3 buckets, and configure lifecycle rules.
2. Create the SQS Main Queue and DLQ, and configure S3 to send event notifications to the queue.
3. Deploy the Lambda functions (including the API Gateway URL generator and the SQS poller) and package the Sharp library using Lambda Layers.
4. Set up AWS Step Functions to orchestrate the processing workflow.
5. Configure the necessary IAM permissions for all services.
6. Set up DynamoDB, the SNS topic, and the CloudFront distribution.
7. Deploy the solution using AWS Console or AWS CLI.

## How to Use
- Request an upload URL via the API Gateway endpoint.
- Upload an image directly to the original S3 bucket using the provided Pre-signed URL.
- The system will asynchronously decouple the event via SQS, and AWS Step Functions will orchestrate the processing steps via Lambda functions.
- Receive an SNS notification once the process succeeds or fails.
- Access the processed images globally with low latency from the CloudFront URL.

## Additional Notes
- The project uses the Sharp library packaged as a **Lambda Layer** for efficient image processing and smaller deployment sizes.
- Security is ensured through fine-grained IAM policies to prevent unauthorized access.
- The architecture is highly resilient; SQS decoupling prevents system overload during traffic spikes and enables retries.
- The project can be extended to support different image formats or additional processing operations.

---

**Project Author:** [sarahalmansouri]  
**Date Created:** [3/7/2026]
