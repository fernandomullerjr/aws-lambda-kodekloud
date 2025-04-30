


1 / 10
info

AWS Lambda: Create a Lambda Function



Welcome to the AWS Lambda hands-on lab. An AWS Cloud account has been created for you as part of this lab.

Use the below credentials to log in to the AWS Management Console:

Console URL 	https://533267452917.signin.aws.amazon.com/console?region=us-east-1
Username 	 
Password 	 
Start Time 	Wed Apr 30 01:20:30 UTC 2025
End Time 	Wed Apr 30 02:20:30 UTC 2025




2 / 10
info

AWS Lambda: Create a Lambda Function


Before attempting the next set of questions, log in to the AWS Console and follow the below steps:

Use the AWS Console to enter the Lambda section.

In the AWS console, enter Lambda in the search bar at the top left hand side of the console screen.

Select Lambda and Select Create Function

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.






3 / 10

AWS Lambda: Create a Lambda Function


How many options are there for creating a Function?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.






4 / 10

AWS Lambda: Create a Lambda Function



In this section, we will use the Author from scratch option to create functions.

Select Author from scratch with the following values and options:
Use kodekloudFunction as the function name.

Use Python 3.9 as the runtime and the default architecture of x86_64.


Expand the Change default execution role tab and select Create a new role with basic Lambda permissions.

Finally, create the function.


Note: The function needs to be created in us-east-1 (N.Virginia) region.

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.

Created the function kodekloudFunction

Runtime - Python3.9






5 / 10

AWS Lambda: Create a Lambda Function



We have created another function named kkFunction. Inspect it.

What is the name of the function handler used?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.


Handler
Info
lambda_function.lambda_handler









6 / 10

AWS Lambda: Create a Lambda Function


Try to Test the kkFunction function now. In the execution results details, what is the status code displayed?

IMPORTANT: Do not change the default Event JSON

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.



Executing function: succeeded (logs )
Details
{
  "statusCode": 200,
  "body": "\"Hello from Kodekloud!!!\""
}






7 / 10

AWS Lambda: Create a Lambda Function


For the kkFunction Lambda function, what is the package size of the function code in bytes?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.


Package size
308 byte





8 / 10

AWS Lambda: Create a Lambda Function


Now, create another Lambda function with name ceaser and the runtime of Nodejs 18.x.

Under change default execution role settings, select Create a new role with basic Lambda permissions.

This function should be created in the us-east-1 (N.Virginia) region.


Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.

Created ceaser function?

Runtime = Nodejs?






9 / 10

AWS Lambda: Create a Lambda Function



What is the default value of timeout in seconds for a Lambda function?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.
