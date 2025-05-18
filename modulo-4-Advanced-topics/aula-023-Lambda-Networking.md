
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