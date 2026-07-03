# SolutionArchitecture-project
aws-graduation-project
# Serverless Image Processing with S3 and Lambda

## Overview
This project aims to create a serverless image processing application where users upload images to an S3 bucket. An AWS Lambda function is automatically triggered to process the images (such as resizing or watermarking) and store the processed versions in another S3 bucket. AWS Step Functions are used to coordinate the workflow of image processing steps.

The AWS services used in this project are:
- Amazon S3 for storing original and processed images.
- AWS Lambda for automatic image processing.
- AWS Step Functions to orchestrate the image processing workflow.
- Amazon DynamoDB for storing metadata about the images.
- Amazon API Gateway to provide an API endpoint for image uploads.
- IAM for securing access to resources.

## Architecture Diagram
<img width="1129" height="301" alt="project" src="https://github.com/user-attachments/assets/0acdb7a3-a2b9-4dd8-b4a3-a98321cc98e8" />



## Features
- Upload images to the original S3 bucket.
- Trigger AWS Lambda to process images (resize, enhance) through Step Functions.
- Store processed images in a separate S3 bucket.
- Secure access with IAM Roles.
- Store image metadata in DynamoDB.
- Use API Gateway to enable image uploads via REST API.

## How to Deploy
1. Set up the original and processed S3 buckets.
2. Deploy the Lambda function and configure it to trigger on image uploads to the original S3 bucket.
3. Set up AWS Step Functions to orchestrate the processing workflow.
4. Configure the necessary IAM permissions.
5. Set up DynamoDB and API Gateway.
6. Deploy the solution using AWS Console or AWS CLI.

## How to Use
- Upload an image to the original S3 bucket.
- AWS Step Functions orchestrate the processing steps via Lambda functions and save the result to the processed S3 bucket.
- Access the processed images from the processed S3 bucket.

## Additional Notes
- The project uses the Sharp library for efficient image processing.
- Security is ensured through fine-grained IAM policies to prevent unauthorized access.
- The project can be extended to support different image formats or additional processing operations.

---

**Project Author:** [sarahalmansouri]  
**Date Created:** [5/6/2025]

---
