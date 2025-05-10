
---


eval $(ssh-agent -s)
ssh-add /home/fernando/.ssh/chave-debian10-github


------------------------------------------------------------------------------------
------------------------------------------------------------------------------------
------------------------------------------------------------------------------------
------------------------------------------------------------------------------------

# Create a Basic Lambda Function using CLI


1 / 10
info

Create a Lambda function using the CLI



Welcome to the AWS Lambda hands-on lab. An AWS Cloud account has been created for you as part of this lab.

Use the below credentials to log in to the AWS Management Console:

Console URL 	https://533266994003.signin.aws.amazon.com/console?region=us-east-1
Username 	kk_labs_user_321187
Password  
Start Time 	Sat May 10 22:46:32 UTC 2025
End Time 	Sat May 10 23:46:32 UTC 2025



You can run the showcreds command anytime to retrieve these credentials.


To display or hide the terminal of the AWS client machine, you can use the expand toggle button as shown below:







2 / 10
info

Create a Lambda function using the CLI


Before attempting the next set of questions, login to the AWS Console and follow the below steps:

Use the AWS Console, enter Lambda section.

In the AWS console enter Lambda in the search bar at the top left hand side of the console screen.



In this lab, we will primarily use the AWS CLI, which has already been configured on the aws-client machine (terminal on the right). To test it, you can run aws lambda help to view the manual page of AWS lambda.

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.






3 / 10

Create a Lambda function using the CLI



How many Lambda functions currently exist in this AWS account (in the us-east-1 region)?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.







4 / 10

Create a Lambda function using the CLI


What is the ARN of the role used for the function called testFunction1?

Note: You can use AWS CLI to retrieve the function details.


arn:aws:lambda:us-east-1:533266994003:function:testFunction1








5 / 10

Create a Lambda function using the CLI



Code for a Lambda function is saved in the file /root/lambda-function.py. Inspect it and determine the function handler that is used.




~ on ☁️  (us-east-1) ➜  cat /root/lambda-function.py
def lambda_handler(event, context):
    if event["name"]== "KodeKloud":
        return "Successful:)"
    else:
        return "Failed :("

~ on ☁️  (us-east-1) ➜  






6 / 10

Create a Lambda function using the CLI



To create a Lambda function using the code present in the lambda-function.py file, it needs to be passed as a zip file.


Create a zip file called my-function.zip using the lambda-function.py file.


use zip command to zip the file.

my-function.zip exists?


- Para zipar:
```bash
zip my-function.zip /root/lambda-function.py
```





7 / 10

Create a Lambda function using the CLI


We now have the zip file of our function code. Next, create the Lambda function with the following details:
function-name: my-function
runtime: python3.9
handler: lambda-function.lambda_handler
role:arn:aws:iam::<your account ID>:role/lambda_execution_role
zip file : path of the zip file


Create the resource only in the us-east-1 region and only use the parameters mentioned above.

Note: Documentation for AWS CLI exists on the top right corner.

Function my-function created?

Runtime - Python3.9

Default timeout - 3 sec

- **Criar a função Lambda:**
comando com o Handler ajustado adequadamente

```bash
aws lambda create-function \
  --function-name my-function \
  --runtime python3.9 \
  --role arn:aws:iam::533266994003:role/lambda_execution_role \
  --handler lambda-function.lambda_handler \
  --zip-file fileb://my-function.zip \
  --region us-east-1
```



~ on ☁️  (us-east-1) ➜  
aws lambda create-function \
  --function-name my-function \
  --runtime python3.9 \
  --role arn:aws:iam::533266994003:role/lambda_execution_role \
  --handler lambda-function.lambda_handler \
  --zip-file fileb://my-function.zip \
  --region us-east-1
{
    "FunctionName": "my-function",
    "FunctionArn": "arn:aws:lambda:us-east-1:533266994003:function:my-function",
    "Runtime": "python3.9",
    "Role": "arn:aws:iam::533266994003:role/lambda_execution_role",
    "Handler": "lambda-function.lambda_handler",
    "CodeSize": 302,
    "Description": "",
    "Timeout": 3,
    "MemorySize": 128,
    "LastModified": "2025-05-10T22:57:31.204+0000",
    "CodeSha256": "F5zeeg+8ilOHpyVmB+g6gED4hi1y/gqlc+3buc8Os88=",
    "Version": "$LATEST",
    "TracingConfig": {
        "Mode": "PassThrough"
    },
    "RevisionId": "3a2b3662-cf21-4027-953a-c26bd2c73549",
    "State": "Pending",
    "StateReason": "The function is being created.",
    "StateReasonCode": "Creating",
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
    "RuntimeVersionConfig": {
        "RuntimeVersionArn": "arn:aws:lambda:us-east-1::runtime:c4127de9acf600313fc596a22245bc413de98744c008a2b8a38abb334f663c06"
    },
    "LoggingConfig": {
        "LogFormat": "Text",
        "LogGroup": "/aws/lambda/my-function"
    }
}

~ on ☁️  (us-east-1) ➜  







8 / 10

Create a Lambda function using the CLI



Navigate to the Lambda section in the AWS Console. Are you able to see the function my-function in the console?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.







9 / 10

Create a Lambda function using the CLI


Now, test the function using CLI, with the payload { "name" : "KodeKloud"} and save the output in the file output.txt.


Test the function in the us-east-1 region.

Note: Use the aws lambda invoke command to test the function using the CLI.

Saved the output in output.txt


- 🧪 **Executar teste simples via CLI**

```bash
aws lambda invoke \
  --function-name my-function \
  --payload '{"name": "KodeKloud"}' \
  --cli-binary-format raw-in-base64-out \
  output.txt
```


~ on ☁️  (us-east-1) ➜  
aws lambda invoke \
  --function-name my-function \
  --payload '{"name": "KodeKloud"}' \
  --cli-binary-format raw-in-base64-out \
  output.txt
{
    "StatusCode": 200,
    "FunctionError": "Unhandled",
    "ExecutedVersion": "$LATEST"
}

~ on ☁️  (us-east-1) ➜  

~ on ☁️  (us-east-1) ➜  cat output.txt 
{"errorMessage": "Unable to import module 'lambda-function': No module named 'lambda-function'", "errorType": "Runtime.ImportModuleError", "requestId": "", "stackTrace": []}
~ on ☁️  (us-east-1) ➜  

~ on ☁️  (us-east-1) ➜  date
Sat May 10 23:12:36 UTC 2025

~ on ☁️  (us-east-1) ➜  





~ on ☁️  (us-east-1) ✖ aws lambda help

~ on ☁️  (us-east-1) ➜  aws lambda list-functions
{
    "Functions": []
}

~ on ☁️  (us-east-1) ➜  

~ on ☁️  (us-east-1) ➜  date
Sat May 10 23:13:58 UTC 2025

~ on ☁️  (us-east-1) ➜  