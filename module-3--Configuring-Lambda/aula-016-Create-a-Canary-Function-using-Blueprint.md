
---


eval $(ssh-agent -s)
ssh-add /home/fernando/.ssh/chave-debian10-github


------------------------------------------------------------------------------------
------------------------------------------------------------------------------------
------------------------------------------------------------------------------------
------------------------------------------------------------------------------------

# Create a Canary Function using Blueprint

Schedule expression
rate(1 day)


canario-de-teste

    Congratulations! Your Lambda function "canario-de-teste" has been successfully created and configured with rule-de-teste-do-canario as a trigger. Choose Test to input a test event and test your function.

Function ARN
arn:aws:lambda:us-east-1:058264180843:function:canario-de-teste


- Código que veio do Blueprint:

~~~~python
import os
from datetime import datetime
from urllib.request import Request, urlopen

SITE = os.environ['site']  # URL of the site to check, stored in the site environment variable
EXPECTED = os.environ['expected']  # String expected to be on the page, stored in the expected environment variable


def validate(res):
    '''Return False to trigger the canary

    Currently this simply checks whether the EXPECTED string is present.
    However, you could modify this to perform any number of arbitrary
    checks on the contents of SITE.
    '''
    return EXPECTED in res


def lambda_handler(event, context):
    print('Checking {} at {}...'.format(SITE, event['time']))
    try:
        req = Request(SITE, headers={'User-Agent': 'AWS Lambda'})
        if not validate(str(urlopen(req).read())):
            raise Exception('Validation failed')
    except:
        print('Check failed!')
        raise
    else:
        print('Check passed!')
        return event['time']
    finally:
        print('Check complete at {}'.format(str(datetime.now())))

~~~~



- Teste com a variável expected setada com valor zoado:
{
  "errorMessage": "Validation failed",
  "errorType": "Exception",
  "requestId": "e86693c6-43a5-4576-996c-5b6e296a4c35",
  "stackTrace": [
    "  File \"/var/task/lambda_function.py\", line 24, in lambda_handler\n    raise Exception('Validation failed')\n"
  ]
}


- Teste com a variável expected setada com valor learn, que é esperado ter no site da KodeKloud:

"1970-01-01T00:00:00Z"

START RequestId: b8ecc4ba-e58e-4f0e-8365-18c263bb2c7e Version: $LATEST
Checking https://www.kodekloud.com/ at 1970-01-01T00:00:00Z...
Check passed!
Check complete at 2025-05-10 23:44:36.824932
END RequestId: b8ecc4ba-e58e-4f0e-8365-18c263bb2c7e
REPORT RequestId: b8ecc4ba-e58e-4f0e-8365-18c263bb2c7e	Duration: 790.39 ms	Billed Duration: 791 ms	Memory Size: 128 MB	Max Memory Used: 47 MB	Init Duration: 127.90 ms	



The retention setting(s) for the following log group(s) have been updated:

    /aws/eks/eks-lab/cluster
    /aws/lambda/canario-de-teste
    /aws/lambda/MinhaLambdaPython-v2
    /aws/lambda/MinhaLambdaPython
    /aws/lambda/myfirstfunctiom