# AWS Translate Capstone Project

## Overview
This project implements a serverless, event-driven language translation pipeline on AWS using Terraform, Lambda, S3, and AWS Translate.  
It automatically translates text from uploaded JSON files and stores the results in a response bucket.

## Architecture
- **S3 Request Bucket:** Receives input JSON files for translation.
- **Lambda Function:** Triggered by new uploads, reads input, calls AWS Translate, and writes output.
- **S3 Response Bucket:** Stores translated JSON files.
- **IAM Role:** Grants Lambda permissions for S3, Translate, and CloudWatch Logs.

## Infrastructure-as-Code
All AWS resources are provisioned using Terraform (`main.tf`):
- S3 buckets with lifecycle policies (auto-expiry)
- IAM role and policy for Lambda
- Lambda function deployment
- S3 event notification trigger

## Lambda Function
- Written in Python (see `lambda.py`)
- Uses Boto3 to interact with S3 and AWS Translate

## Usage

1. **Clone the repository**
2. **Deploy infrastructure:**
   ```sh
   terraform init
   terraform apply
   ```
3. **Package Lambda:**
   - Zip your `lambda.py` as `lambda.zip`
   - Place `lambda.zip` in the project root
4. **Upload a sample JSON to the request bucket**
5. **Check the response bucket for translated output**

## Sample Input JSON
```json
{
  "SourceLanguageCode": "en",
  "TargetLanguageCode": "fr",
  "TextList": ["Hello world!", "How are you?"]
}
```

## Cleanup
```sh
terraform destroy
```

## Deliverables
- Terraform template (`main.tf`)
- Lambda function (`lambda.py`)
- Sample JSON files
- Documentation (this file)

## Troubleshooting
- Ensure AWS credentials are configured
- Check CloudWatch Logs for Lambda errors
- See comments in `main.tf` for resource details

## License
MIT
