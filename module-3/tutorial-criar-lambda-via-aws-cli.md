Aqui está um exemplo simples de uma AWS Lambda em Python e os comandos AWS CLI para empacotar e fazer o deploy.

---

## 🐍 **Exemplo de código Lambda em Python (arquivo `lambda_function.py`)**

```python
def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': 'Olá, Lambda em Python funcionando!'
    }
```

---

## 📦 **Empacotar a função Lambda**

Crie um arquivo `.zip` com o código (e dependências, se houver):

```bash
zip lambda_function.zip lambda_function.py
```

Se você tiver dependências, use um virtualenv e adicione ao `.zip`:

```bash
pip install -r requirements.txt -t package/
cd package
zip -r ../lambda_function.zip .
cd ..
zip -g lambda_function.zip lambda_function.py
```

---

## 🚀 **Comandos AWS CLI para deploy**

1. **Criar a função Lambda:**

```bash
aws lambda create-function \
  --function-name MinhaLambdaPython \
  --runtime python3.11 \
  --role arn:aws:iam::<SEU-ID-CONTA>:role/<ROLE-LAMBDA> \
  --handler lambda_function.lambda_handler \
  --zip-file fileb://lambda_function.zip \
  --region us-east-1
```

2. **Atualizar código de uma função já existente:**

```bash
aws lambda update-function-code \
  --function-name MinhaLambdaPython \
  --zip-file fileb://lambda_function.zip \
  --region us-east-1
```

---

## 🧪 **Executar teste simples via CLI**

```bash
aws lambda invoke \
  --function-name MinhaLambdaPython \
  --payload '{}' \
  resposta.json
cat resposta.json
```

---

Quer um exemplo com API Gateway ou com dependências como `requests`?