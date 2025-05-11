
---


eval $(ssh-agent -s)
ssh-add /home/fernando/.ssh/chave-debian10-github


------------------------------------------------------------------------------------
------------------------------------------------------------------------------------
------------------------------------------------------------------------------------
------------------------------------------------------------------------------------

# Lab: Lambda function with CLI and Blueprint



1 / 11
info

Create a Lambda function using a blueprint



Welcome to the AWS Lambda hands-on lab. An AWS Cloud account has been created for you as part of this lab.

Use the below credentials to log in to the AWS Management Console:

Console URL 	https://058264544314.signin.aws.amazon.com/console?region=us-east-1
Username 	kk_labs_user_214858
Password 	 
Start Time 	Sun May 11 18:51:26 UTC 2025
End Time 	Sun May 11 19:51:26 UTC 2025



You can run the showcreds command anytime to retrieve these credentials.


To display or hide the terminal of the AWS client machine, you can use the expand toggle button as shown below:





2 / 11
info

Create a Lambda function using a blueprint


Before attempting the next set of questions, log in to the AWS Console and follow the below steps:

Use the AWS Console to enter the Lambda section.

In the AWS console, enter Lambda in the search bar at the top left hand side of the console screen.

Select Lambda to enter the Lambda section.

Note: You can retrieve the AWS Credentials for your account at anytime by running the showcreds command.




3 / 11

Create a Lambda function using a blueprint



How many Lambda functions currently exist in the environment now (in the us-east-1 region)?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.






4 / 11

Create a Lambda function using a blueprint



What is the runtime used for the function called test_func2?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.



Runtime settings  Info

Runtime
    Ruby 3.2






5 / 11

Create a Lambda function using a blueprint


Let us now create a function using a Blueprint.


Create a function with name HelloWorld using an existing template.

Make sure the function uses a python runtime.

Create the function only in the us-east-1 (N.Virginia) region.

For the execution role, select Create a new role with basic Lambda permissions

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.

Function -HelloWorld created?

Runtime - python





6 / 11
info

Create a Lambda function using a blueprint



We will now create a canary function that will periodically check for a text inside a site we specify within the function definition.

We will use an existing blueprint for accomplishing the task.






7 / 11

Create a Lambda function using a blueprint

Create a new function using an existing blueprint.


In the select blueprint drop-down, search for Schedule a periodic check of any URL.

Create a function kkCanaryFunction using the above blueprint.

If asked for trigger rules, select or create a new rule minuteRule that will schedule a trigger for every minute. Use rate(1 minute) for schedule expression.

Resource must be created in the us-east-1 (N.Virginia) region.



Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.

Function - kkCanaryFunction created?

Trigger rule - minuteRule created?

rate - 1 minute?





8 / 11

Create a Lambda function using a blueprint

What is the ARN for the minuteRule that was configured earlier?

Note: You can use CLI also for getting ARN



~ on ☁️  (us-east-1) ➜  aws lambda list-functions
{
    "Functions": [
        {
            "FunctionName": "kkCanaryFunction",
            "FunctionArn": "arn:aws:lambda:us-east-1:058264544314:function:kkCanaryFunction",
            "Runtime": "python3.10",
            "Role": "arn:aws:iam::058264544314:role/service-role/kkCanaryFunction-role-vywzijr7",
            "Handler": "lambda_function.lambda_handler",
            "CodeSize": 654,
            "Description": "Performs a periodic check of the given site, erroring out on test failure.",
            "Timeout": 10,
            "MemorySize": 128,
            "LastModified": "2025-05-11T19:04:35.379+0000",
            "CodeSha256": "oh0RwNg498ywub/x2h2K1S2s6ALUld6PbHPpi/H0/eU=",
            "Version": "$LATEST",
            "Environment": {
                "Variables": {
                    "site": "https://www.amazon.com/",
                    "expected": "Online Shopping"
                }
            },
            "TracingConfig": {
                "Mode": "PassThrough"
            },
            "RevisionId": "d050a807-4da0-4e14-aa8c-1295663ddfb6",
            "PackageType": "Zip",
            "Architectures": [
                "x86_64"
            ],
            "EphemeralStorage": {
                "Size": 512
            },
            "SnapStart": {
                "ApplyOn": "None",
                "OptimizationStatus": "Off"
            },
            "LoggingConfig": {
                "LogFormat": "Text",
                "LogGroup": "/aws/lambda/kkCanaryFunction"
            }
        }
    ]
}

~ on ☁️  (us-east-1) ➜  



~ on ☁️  (us-east-1) ➜  aws events list-rules
{
    "Rules": [
        {
            "Name": "EKSComputeManagedRule",
            "Arn": "arn:aws:events:us-east-1:058264544314:rule/EKSComputeManagedRule",
            "EventPattern": "{\"source\": [\"aws.ec2\", \"aws.health\"],\"detail-type\":[\"EC2 Spot Instance Interruption Warning\", \"EC2 Instance State-change Notification\", \"EC2 Instance Rebalance Recommendation\", \"AWS Health Event\"]}",
            "State": "ENABLED",
            "Description": "EKSComputeManagedRule",
            "ManagedBy": "eks.amazonaws.com",
            "EventBusName": "default"
        },
        {
            "Name": "codepipeline-15955121-sourcewebdeepan-rule",
            "Arn": "arn:aws:events:us-east-1:058264544314:rule/codepipeline-15955121-sourcewebdeepan-rule",
            "EventPattern": "{\"source\":[\"aws.s3\"],\"detail-type\":[\"AWS API Call via CloudTrail\"],\"detail\":{\"eventSource\":[\"s3.amazonaws.com\"],\"eventName\":[\"PutObject\",\"CompleteMultipartUpload\",\"CopyObject\"],\"requestParameters\":{\"bucketName\":[\"source-web-deepan\"],\"key\":[\"my-website.zip\"]}}}",
            "State": "ENABLED",
            "Description": "Amazon CloudWatch Events rule to automatically start your pipeline when a change occurs in the Amazon S3 object key or S3 folder. Deleting this may prevent changes from being detected in that pipeline. Read more: http://docs.aws.amazon.com/codepipeline/latest/userguide/pipelines-about-starting.html",
            "EventBusName": "default"
        },
  {
            "Name": "minuteRule",
            "Arn": "arn:aws:events:us-east-1:058264544314:rule/minuteRule",
            "State": "ENABLED",
            "Description": "minuteRule",
            "ScheduleExpression": "rate(1 minute)",
            "EventBusName": "default"
        }
    ]
}
(END)