# Create Stack
- **Deploy Stack**
    ```bash
    aws cloudformation deploy --stack-name s3-web --template-file s3-web/cdnBucket.yml --parameter-overrides EnvironmentName=QA1
    ```

- ** Upload Web Site to S3 Bucket**
    ```s3
    aws s3 cp ./s3-web/docroot/ s3://$(aws cloudformation describe-stacks --stack-name s3-web --query 'Stacks[0].Outputs[?ExportName==`QA1-bucketName`].OutputValue' --output text)/ --recursive
    ```
---
# Delete Stack
- **Empty the bucket**
    ```bash
    aws s3 rm s3://$(aws cloudformation describe-stacks --stack-name s3-web --query 'Stacks[0].Outputs[?ExportName==`QA1-bucketName`].OutputValue' --output text) --recursive
    ```
- **Delete Stacks**
    ```bash
    aws cloudformation delete-stack --stack-name s3-web
    ```

# Info
- **Get Bucket Name**
    ```s3
    aws cloudformation describe-stacks --stack-name s3-web --query 'Stacks[0].Outputs[?ExportName==`QA1-bucketName`].OutputValue' --output text

    aws s3 ls $(aws cloudformation describe-stacks --stack-name s3-web --query 'Stacks[0].Outputs[?ExportName==`QA1-bucketName`].OutputValue' --output text)
    ```
