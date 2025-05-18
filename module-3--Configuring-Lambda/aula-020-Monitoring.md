## Monitoring

AWS Lambda oferece integração com **CloudWatch** e **X-Ray** para monitoramento e troubleshooting.

### CloudWatch

- Monitora:
  - Número de invocações
  - Duração de cada requisição
  - Erros
  - Outras métricas relevantes

### Lambda Insights

- Extensão adicional do CloudWatch
- Fornece informações agregadas sobre todas as funções Lambda em sua conta ou região

### X-Ray

- Ferramenta de monitoramento e solução de problemas
- Permite visualizar requisições conforme percorrem sua aplicação
- Ajuda a identificar gargalos e erros

### Monitoramento de Rede

- Informações sobre tráfego TCP/IP e rede **não estão disponíveis por padrão**
- Essas informações podem estar acessíveis por meio de **VPC Flow Logs**, caso a Lambda esteja executando dentro de uma **VPC**
