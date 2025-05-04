
---


------------------------------------------------------------------------------------

# Create a Basic Lambda Function using CLI


aws configure


- Arquivo em Python criado anteriormente para uso na aula:
/home/fernando/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction/basichelloworld.py

~~~~python
def lambda_handler(event, context):
    if event["name"] == "KodeKloud":
        return "Successful"
~~~~


- Crie um arquivo `.zip` com o código (e dependências, se houver):

```bash
cd /home/fernando/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction
zip lambda_function.zip basichelloworld.py
```

- Verificando:

~~~~bash

fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$ zip lambda_function.zip basichelloworld.py
  adding: basichelloworld.py (deflated 10%)
fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$
fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$ ls -lhasp
total 16K
4.0K drwxr-xr-x 2 fernando fernando 4.0K May  4 15:34 ./
4.0K drwxr-xr-x 3 fernando fernando 4.0K May  4 15:02 ../
4.0K -rw-r--r-- 1 fernando fernando  100 Apr 29 22:44 basichelloworld.py
4.0K -rw-r--r-- 1 fernando fernando  276 May  4 15:34 lambda_function.zip
fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$

~~~~




- Erro:

~~~~bash
fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$ aws lambda create-function \
>   --function-name MinhaLambdaPython \
>   --runtime python3.9 \
>   --handler lambda_function.lambda_handler \
>   --zip-file fileb://lambda_function.zip \
>   --region us-east-1

usage: aws [options] <command> <subcommand> [<subcommand> ...] [parameters]
To see help text, you can run:

  aws help
  aws <command> help
  aws <command> <subcommand> help

aws: error: the following arguments are required: --role

fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$

~~~~


- Criando role com permissoes basicas
arn:aws:iam::058264180843:role/lambda-role-testes


- **Criar a função Lambda:**
ajustando o comando

```bash
aws lambda create-function \
  --function-name MinhaLambdaPython \
  --runtime python3.9 \
  --role arn:aws:iam::058264180843:role/lambda-role-testes \
  --handler lambda_function.lambda_handler \
  --zip-file fileb://lambda_function.zip \
  --region us-east-1
```


- Resultado:

```bash

fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$ aws lambda create-function \
>   --function-name MinhaLambdaPython \
>   --runtime python3.9 \
>   --role arn:aws:iam::058264180843:role/lambda-role-testes \
>   --handler lambda_function.lambda_handler \
>   --zip-file fileb://lambda_function.zip \
>   --region us-east-1
{
    "FunctionName": "MinhaLambdaPython",
    "FunctionArn": "arn:aws:lambda:us-east-1:058264180843:function:MinhaLambdaPython",
    "Runtime": "python3.9",
    "Role": "arn:aws:iam::058264180843:role/lambda-role-testes",
    "Handler": "lambda_function.lambda_handler",
    "CodeSize": 276,
    "Description": "",
    "Timeout": 3,
    "MemorySize": 128,
    "LastModified": "2025-05-04T18:38:54.586+0000",
    "CodeSha256": "Zy2+QbsVg7dmSrdA2u2lG7NDKjagVj+2th0jl/918yY=",
    "Version": "$LATEST",
    "TracingConfig": {
        "Mode": "PassThrough"
    },
    "RevisionId": "0030aafb-435d-4c61-bf03-c99fa753dad2",
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
        "RuntimeVersionArn": "arn:aws:lambda:us-east-1::runtime:c88c82727548b4b718883e305881b033842dceea07a5c4914a1258f41c91d3b7"
    }
}
fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$
fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$
fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$ date
Sun 04 May 2025 03:38:57 PM -03
fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$
```



- 🧪 **Executar teste simples via CLI**

```bash
aws lambda invoke \
  --function-name MinhaLambdaPython \
  --payload '{"name": "KodeKloud"}' \
  resposta.json
cat resposta.json
```


- Erro:

```bash

fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$
fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$ aws lambda invoke \
>   --function-name MinhaLambdaPython \
>   --payload '{"name": "KodeKloud"}' \
>   resposta.json

Invalid base64: "{"name": "KodeKloud"}"
```


O erro `Invalid base64: "{"name": "KodeKloud"}"` indica que o valor passado para a opção `--payload` precisa estar codificado em base64 **apenas se você estiver usando a CLI em modo de linha bruta (`--cli-binary-format raw-in-base64-out`)**, o que depende da versão da AWS CLI.

### Solução:

#### ✅ Se estiver usando AWS CLI **v2**, adicione a opção:

```bash
--cli-binary-format raw-in-base64-out
```

Portanto, o comando completo fica assim:

```bash
aws lambda invoke \
  --function-name MinhaLambdaPython \
  --payload '{"name": "KodeKloud"}' \
  --cli-binary-format raw-in-base64-out \
  resposta.json
```

---

#### ❌ Se você **não** usar `--cli-binary-format`, o padrão é `base64`, e então você teria que codificar manualmente o JSON, o que não é prático.

### Verifique sua versão da AWS CLI:

```bash
aws --version
```

Se for AWS CLI v2 (ex: `aws-cli/2.11.4`), o uso do `--cli-binary-format` é o recomendado.

Deseja ajuda para testar se a função Lambda está retornando corretamente no `resposta.json`?




- 🧪 **Executar teste simples via CLI**

```bash
aws lambda invoke \
  --function-name MinhaLambdaPython \
  --payload '{"name": "KodeKloud"}' \
  --cli-binary-format raw-in-base64-out \
  resposta.json
cat resposta.json
```


OK

agora funcionou o teste:

~~~~bash

fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$ aws lambda invoke \
>   --function-name MinhaLambdaPython \
>   --payload '{"name": "KodeKloud"}' \
>   --cli-binary-format raw-in-base64-out \
>   resposta.json
{
    "StatusCode": 200,
    "FunctionError": "Unhandled",
    "ExecutedVersion": "$LATEST"
}
fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$ date
Sun 04 May 2025 03:45:29 PM -03
fernando@debian10x64:~/cursos/aws/aws-lambda-kodekloud/module-3--Configuring-Lambda/basicfunction$

~~~~