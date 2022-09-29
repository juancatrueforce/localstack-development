# [LOCALSTACK](https://github.com/localstack/localstack) WITH DOCKER COMPOSE

I hope this repo will be usefull for you, the reason this repo is that you can use functions of aws on local in your development environment.

## Requirements
- [Docker](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-debian-10)
- [Docker Compose](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-22-04)
- [AWS Client](https://gist.github.com/anamorph/aaf8434d3bbad92059b3)


## Installation
The steps for get **localstack** are as follows:

1. Running LocalStack with docker compose, into root project's folder execute the following.
    ```bash 
    docker-compose up -d
    ```

2. Verify your localstack is running, go to [http://localhost:4566/health](http://localhost:4566/health)
You should see somthing similar to the following
    ```bash 
    {"features": {"initScripts": "initialized"}, "services": {"acm": "available", "apigateway": "available", "cloudformation": "available", "cloudwatch": "available", "config": "available", "dynamodb": "available", "dynamodbstreams": "available", "ec2": "available", "es": "available", "events": "available", "firehose": "available", "iam": "available", "kinesis": "available", "kms": "available", "lambda": "available", "logs": "available", "opensearch": "available", "redshift": "available", "resource-groups": "available", "resourcegroupstaggingapi": "available", "route53": "available", "route53resolver": "available", "s3": "available", "s3control": "available", "secretsmanager": "available", "ses": "available", "sns": "available", "sqs": "available", "ssm": "available", "stepfunctions": "available", "sts": "available", "support": "available", "swf": "available"}, "version": "0.14.5.dev"}
    ```
3. Enter to localstack container
    ```bash
    docker exec -it localstack bash
    ```

4. Once inside you have to initialize the aws:
    ```bash
    aws configure
    ```
    Set AWS Access Key ID, AWS Secret Access Key,  Default region name and Default output format, such as the following:
    ```bash
    AWS Access Key ID [None]: foo
    AWS Secret Access Key [None]: bar
    Default region name [None]: us-west-2 
    Default output format [None]: 
    ```
    You can use the same command to re set the credentials.

5. Verify your settings using the following command:
    ```bash
    aws configure list
    ```
    you can see something like this:
    ```bash
          Name                    Value             Type    Location
          ----                    -----             ----    --------
      profile                <not set>             None    None
    access_key      ****************foo shared-credentials-file    
    secret_key      ****************bar shared-credentials-file    
        region                us-west-2      config-file    ~/.aws/config
    ```

6. Create your first bucket typing the following:
    ```bash
    awslocal s3 mb s3://bucket-demo
    ```
7. Verify that existing your new bucket typing the following:
    ```bash
    awslocal s3 ls
    ```
    Also you can verify from out of the container with the following:
    ```bash
    aws --endpoint-url=http://localhost:4566 s3 ls
    ```
    You have to see something like this:
    ```bash
    2022-09-29 11:42:43 bucket-demo
    ```
8. Now you can upload files to your new bucket of AWS without spending money. Typing the following(**localstack-readme-banner.svg** is my test file you can use other file to upload):
   ```bash
   aws --endpoint-url=http://localhost:4566 s3 cp localstack-readme-banner.svg s3://bucket-demo
   ```



  