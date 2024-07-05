# AWS_cloudformation_example
A simple CloudFormation example on local.


# INTRO

- This is a simple Cloud Formation example to build and validate a stack.

# SETUP

- Make sure the aws cli is updated to the latest version (2.17.x in this example): https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html#getting-started-install-instructions

- Configure the aws cli: https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html

# CREATE

- create a cloud formation example.

```
AWSTemplateFormatVersion: '2010-09-09'
Description: A simple example CloudFormation template

Resources:
  MyS3Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: my-cloudformation-example-bucket
```

# VALIDATE

- Validate the cloud formation example.

```
aws cloudformation validate-template --template-body file://cf_example.yaml
```

# CREATE STACK

- Create the stack locally for testing purposes. This will create a changeset while not creating the actual resources.

```
aws cloudformation create-stack --stack-name my-example-stack --template-body file://cf_example.yaml

{
    "StackId": "arn:aws:cloudformation:us-east-2:123456789:stack/my-example-stack/123456-7890-1234-5678-01234567890"
}

```

- Then List the stacks to confirm creation:

```
aws cloudformation describe-stacks

{
    "Stacks": [
        {
            "StackId": "arn:aws:cloudformation:us-east-2:123456789:stack/my-example-stack/123456-7890-1234-5678-01234567890",
            "StackName": "my-example-stack",
            "Description": "A simple example CloudFormation template",
            "CreationTime": "2024-07-05T12:25:07.440000+00:00",
            "RollbackConfiguration": {},
            "StackStatus": "CREATE_IN_PROGRESS",
            "DisableRollback": false,
            "NotificationARNs": [],
            "Capabilities": [
                "CAPABILITY_IAM"
            ],
            "Tags": [],
            "EnableTerminationProtection": false,
            "DriftInformation": {
                "StackDriftStatus": "NOT_CHECKED"
            }
        }
    ]
}
```

- Then delete the example stack:

```

aws cloudformation delete-stack --stack-name my-example-stack

```

- Then List the stacks to confirm removed:

```
aws cloudformation describe-stacks

{
    "Stacks": []
}
```

