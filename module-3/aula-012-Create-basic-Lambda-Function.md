
eval $(ssh-agent -s)
ssh-add /home/fernando/.ssh/chave-debian10-github


- Criar Lambda em Python 3.9

código original

~~~~python
import json

def lambda_handler(event, context):
    # TODO implement
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda!')
    }
~~~~



- Ajustando

~~~~python
import json

def lambda_handler(event, context):
    if event["name"] == "KodeKloud":
        return "Successful"
~~~~



KodeKloudtest

~~~~json
{
  "key1": "value1",
  "key2": "value2",
  "key3": "value3"
}
~~~~



~~~~json
{
  "name": "KodeKloud"
}
~~~~


START RequestId: f4eba93d-6529-4908-b7d6-d4e2ae6cbcf5 Version: $LATEST
END RequestId: f4eba93d-6529-4908-b7d6-d4e2ae6cbcf5
REPORT RequestId: f4eba93d-6529-4908-b7d6-d4e2ae6cbcf5	Duration: 2.60 ms	Billed Duration: 3 ms	Memory Size: 128 MB	Max Memory Used: 31 MB	Init Duration: 75.25 ms	


Executing function: succeeded (logs )
Details
"Successful"