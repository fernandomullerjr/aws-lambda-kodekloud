
# Event Sources

- No modelo Asynchronous, a Lambda trabalha com as retentativas("Retries").

- Importante adicionar no código como vai lidar com os Erros e a Retentativas.

- 3 tentativas
1 minuto entre a primeira e segunda tentativa
2 minutos entre a segunda e terceira tentativa
se mesmo assim falhar, é possível enviar o Evento da Lambda para uma Dead Letter Queue




### Push Model Source Types

- Synchronous
Cloudformation
Cloudfront
API Gateway
Cognito

- Asynchronous
Cloudwatch 
Eventbridge
S3 
SNS



### Pull Model Source Types

- Streams 
Dynamo DB 
Kinesis Data Stream

- Queues
Amazon Simple Queueing Service