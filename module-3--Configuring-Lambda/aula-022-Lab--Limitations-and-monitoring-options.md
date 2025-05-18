
---


eval $(ssh-agent -s)
ssh-add /home/fernando/.ssh/chave-debian10-github


------------------------------------------------------------------------------------
------------------------------------------------------------------------------------
------------------------------------------------------------------------------------
------------------------------------------------------------------------------------

# Lab: Limitations and monitoring options


1 / 13
info

AWS Lambda: Limitations and Monitoring



Welcome to the AWS Lambda hands-on lab. An AWS Cloud account has been created for you as part of this lab.

Use the below credentials to log in to the AWS Management Console:

Console URL 	https://774305609903.signin.aws.amazon.com/console?region=us-east-1
Username 	kk_labs_user_407911
Password 	 
Start Time 	Sun May 18 01:18:44 UTC 2025
End Time 	Sun May 18 02:18:44 UTC 2025



You can run the showcreds command anytime to retrieve these credentials.
`

To display or hide the terminal of the AWS client machine, you can use the expand toggle button as shown below:
toggle button





2 / 13

Lambda Limitations

How many Lambda functions exist in the current user session?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.




3 / 13

AWS Lambda: Limitations



What is the default minimum and maximum timeout for the Lambda function?

Note: You can retrieve the AWS Credentials for your account at anytime by running the showcreds command.



1 segundo
e 900 segundos




4 / 13

AWS Lambda: Limitations



What is the timeout (in seconds) set for existing Lambda function called kk_lambda_test1 (us-east-1 region)?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.





5 / 13

AWS Lambda: Limitations



What is the maximum memory size that can be configured to a Lambda function?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.




6 / 13

AWS Lambda: Limitations



What is the memory size allocated to the existing lambda the function kk_lambda_test2 ?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.



7 / 13

AWS Lambda: Limitations



What is the value of Ephemeral Size that is for the function kk_lambda_test3 ?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.





8 / 13

AWS Lambda: Limitations



How many Lambda functions can run concurrently by default in a region and in an account?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.


1 thousand






9 / 13

AWS Lambda: Limitations



How do you increase the concurrency limit?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.


open quota case




10 / 13

AWS Lambda: Monitoring



Which AWS service can be used for monitoring Lambda metrics?


both: Cloudwatch and X-ray




11 / 13

AWS Lambda: Monitoring



Which AWS service is configured by default to collect logs and standard metrics from a Lambda function?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.






12 / 13

AWS Lambda: Monitoring



Which of the following are types of Lambda metrics?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.


concurrency, invocation, performance



13 / 13

AWS Lambda: Monitoring



Which AWS service can provide a visual map of the application path for Lambda?

Note: You can retrieve the AWS Credentials for your account anytime by running the showcreds command.

x-ray