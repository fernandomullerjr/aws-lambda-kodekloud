
---


eval $(ssh-agent -s)
ssh-add /home/fernando/.ssh/chave-debian10-github


------------------------------------------------------------------------------------
------------------------------------------------------------------------------------
------------------------------------------------------------------------------------
------------------------------------------------------------------------------------

# Lambda Networking


- Quando a Lambda está no default, a VPC é gerenciada pela AWS, que garante a mesma disponibilidade dos demais serviços gerenciados por ela.

- Quando colocada em VPC privada própria, a responsabilidade pela disponibilidade é nossa.

- Para falar com a internet, é necessário adicionar um NAT Gateway, quando temos a Lambda na nossa VPC Privada.

- Cada Lambda na VPC gera uma ENI.

- Existe limite de ENI por região.

- Outra opção para conectar uma Lambda que está na VPC Default com Lambdas das VPC's Privadas é usando um Interface Endpoint.