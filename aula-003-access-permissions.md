

# Access Permissions

Access Permissions

Security is crucial when dealing with Lambda because of its
power to run code and take actions that affect other AWS
services.

Two types of security permissions are needed for Lambda:
Invocation permissions and Execution roles.

Invocation permissions are only needed for push event
sources and are granted through an IAM resource policy
automatically created when configuring an AWS service as an
event source.

Execution roles grant Lambda permissions to interact with
other AWS services. They include an IAM policy defining what
Lambda is allowed to do and a Trust policy allowing Lambda
to assume the execution role and perform actions on the
other service.
Adding the execution role to your Lambda function is the
final step in granting permissions and policies.