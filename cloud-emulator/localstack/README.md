# localstack

Impersonate AWS Stack

Quickstart: https://docs.localstack.cloud/getting-started/quickstart/

## Kinesis
```
awslocal kinesis list-streams
```

## Lambda
```
awslocal lambda list-functions
```

## Create the S3 buckets
```
awslocal s3 mb s3://localstack-thumbnails-app-images
awslocal s3 mb s3://localstack-thumbnails-app-resized
```

## List S3 Buckets
```
awslocal s3api list-buckets
```

## Create SNS DLQ Topic for failed lambda invocations
```
awslocal sns create-topic --name failed-resize-topic
```

To receive immediate alerts in case of image resize failures, subscribe an email address to the system. You can use the following command to subscribe an email address to the SNS topic:
```
awslocal sns subscribe \
 --topic-arn arn:aws:sns:us-east-1:000000000000:failed-resize-topic \
 --protocol email \
 --notification-endpoint my-email@example.com
```

## Create the Presign Lambda
```
(cd lambdas/presign; rm -f lambda.zip; zip lambda.zip handler.py)
awslocal lambda create-function \
    --function-name presign \
    --runtime python3.11 \
    --timeout 10 \
    --zip-file fileb://lambdas/presign/lambda.zip \
    --handler handler.handler \
    --role arn:aws:iam::000000000000:role/lambda-role \
    --environment Variables="{STAGE=local}"
awslocal lambda wait function-active-v2 --function-name presign
awslocal lambda create-function-url-config \
    --function-name presign \
    --auth-type NONE
```

## Create the Image List Lambda
```
(cd lambdas/list; rm -f lambda.zip; zip lambda.zip handler.py)
awslocal lambda create-function \
    --function-name list \
    --handler handler.handler \
    --zip-file fileb://lambdas/list/lambda.zip \
    --runtime python3.11 \
    --timeout 10 \
    --role arn:aws:iam::000000000000:role/lambda-role \
    --environment Variables="{STAGE=local}"
awslocal lambda wait function-active-v2 --function-name list
awslocal lambda create-function-url-config \
    --function-name list \
    --auth-type NONE
```

## Build the Image Resizer Lambda
```
cd lambdas/resize
rm -rf libs lambda.zip
docker run --platform linux/x86_64 -v "$PWD":/var/task "public.ecr.aws/sam/build-python3.11" /bin/sh -c "pip install -r requirements.txt -t libs; exit"
cd libs && zip -r ../lambda.zip . && cd ..
zip lambda.zip handler.py
rm -rf libs
cd ../..
```

## Create the Image Resizer Lambda
```
awslocal lambda create-function \
    --function-name resize \
    --runtime python3.11 \
    --timeout 10 \
    --zip-file fileb://lambdas/resize/lambda.zip \
    --handler handler.handler \
    --dead-letter-config TargetArn=arn:aws:sns:us-east-1:000000000000:failed-resize-topic \
    --role arn:aws:iam::000000000000:role/lambda-role \
    --environment Variables="{STAGE=local}"
awslocal lambda wait function-active-v2 --function-name resize
awslocal lambda put-function-event-invoke-config \
    --function-name resize \
    --maximum-event-age-in-seconds 3600 \
    --maximum-retry-attempts 0
```

## Connect S3 bucket to Resizer Lambda
```
awslocal s3api put-bucket-notification-configuration \
 --bucket localstack-thumbnails-app-images \
 --notification-configuration "{\"LambdaFunctionConfigurations\": [{\"LambdaFunctionArn\": \"$(awslocal lambda get-function --function-name resize --output json | jq -r .Configuration.FunctionArn)\", \"Events\": [\"s3:ObjectCreated:*\"]}]}"
```

## Create the S3 static website
```
awslocal s3 mb s3://webapp
awslocal s3 sync --delete ./website s3://webapp
awslocal s3 website s3://webapp --index-document index.html
```

## Retrieve the Lambda Function URLs
```
awslocal lambda list-function-url-configs --function-name presign --output json | jq -r '.FunctionUrlConfigs[0].FunctionUrl'
awslocal lambda list-function-url-configs --function-name list --output json | jq -r '.FunctionUrlConfigs[0].FunctionUrl'
```