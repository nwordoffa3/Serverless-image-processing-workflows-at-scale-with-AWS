# README.md for AWS Step Functions Workshop at AWS GOTO EDA 2023

## Overview

This project was developed during the AWS GOTO EDA 2023 conference in Nashville. It demonstrates how to build a deep learning image profile application by orchestrating multiple AWS services using AWS Step Functions. The services involved include Amazon DynamoDB, Amazon S3, Amazon Rekognition, and AWS Lambda.

The application is designed to:

1. Validate an image from an S3 bucket to ensure it contains a single face.
2. Check if the face is a duplicate in the existing collection.
3. Create an index for the face.
4. Resize the image.
5. Store the metadata in a DynamoDB table.

## Workflow

The Step Function JSON configuration contains multiple states, which are mainly AWS Lambda functions. Each state has its own responsibilities:

### States

1. **Face Detection**: Validates the image to ensure it has only one face.
2. **Check Face Duplicate**: Verifies if the face already exists in the collection.
3. **Parallel Processing**: Adds the face to an index and resizes the image concurrently.
4. **Persist Metadata**: Saves the metadata of the image to a DynamoDB table.
5. **Photo Does Not Meet Requirement**: Error handling state, which sends notifications via SNS.

## Pre-requisites

1. AWS Account
2. AWS CLI
3. AWS Step Functions configured
4. AWS Lambda functions for each state
5. Amazon DynamoDB table
6. Amazon S3 bucket with images
7. Amazon SNS for notifications

## How to Deploy

1. Upload your image to the specified S3 bucket.
2. Trigger the AWS Step Functions state machine.

## Error Handling

Retry logic and error catching are implemented for each Lambda function. If the Lambda function fails due to service exceptions or too many requests, the function will retry according to the specified policy.

## Notifications

The `Photo Does Not Meet Requirement` state will publish a message to an SNS topic if the image is invalid or if the face is a duplicate.

## Conclusion

This application showcases the power of AWS Step Functions to coordinate multiple AWS services into a scalable and maintainable application.

Feel free to fork, contribute, and reach out with any questions or improvements.
