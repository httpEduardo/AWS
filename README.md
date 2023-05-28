# AWS

NOTA: Este repositório não está sendo mantido ativamente. Entre em contato com seu representante HashiCorp ou líder da comunidade para obter as últimas informações sobre a instalação do Vault na AWS.

## Introdução

Este repositório contém código para criar Amazon Machine Images (AMI) e um modelo Cloudformation genérico. A AMI e o modelo podem ser usados para criar um cluster Vault pronto para produção.

## O que ele constrói?

Os templates do Cloudformation publicados por este pipeline possuem a seguinte configuração:

- VPC com 3 sub-redes públicas e 3 privadas
- Sistema operacional para Vault e Consul é o Centos 7
- O sistema operacional para o host Bastion é AWS Linux (mais recente)
- 3 servidores Vault e 5 servidores Consul distribuídos pelas sub-redes privadas
- Um bastion host para conexão com outros servidores, que não são diretamente acessíveis pela Internet
- Um certificado SSL real vinculado ao seu FQDN, gerenciado pelo Amazon Certificate Manager
- Abertura automática do Vault usando o AWS Key Management Service para armazenar a chave de abertura
- O cluster do Vault estará pronto em 10 a 15 minutos. O cluster surge em um estado não inicializado. A API atende na porta 8200 e pode ser acessada pela Internet.

## Instruções de uso

* Crie AMIs para Vault e Consul usando os modelos Packer incluídos.
* Edite o arquivo cloudformation/aws_vault_cf.yml e insira seus novos valores para as AMIs.
* OPCIONAL: Tenha um domínio (ou subdomínio) de sua propriedade no gerenciamento do AWS Route 53. Isso permite automatizar a criação de registros DNS que apontam para o cluster do Vault. Também permite validar automaticamente o certificado SSL.
* Use a IU do AWS Cloudformation para carregar seu arquivo aws_vault_cf.yml, preencha todos os valores necessários e crie uma nova pilha. Certifique-se e verifique o registro DNS que você usou para o cluster Vault no Route 53 (ou criando um registro DNS TXT em seu próprio provedor DNS).
* Após cerca de 15 minutos, seu cluster do Vault estará pronto para a configuração inicial. Você pode usar 1 e 1 para os compartilhamentos de chaves iniciais e compartilhamentos de recuperação. Salve o token raiz inicial e a chave de recuperação em um local seguro.
* Faça login no cluster do Vault usando o token raiz e configure o Vault.
#AWS
