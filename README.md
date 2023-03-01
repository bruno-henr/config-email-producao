# rockeseat-config-email-producao
Apenas um readme com os passos necessarios para configurar um email em producao

1º config
Utilizar SES da AWS para disparar emails
- Possuir um dominio (ex.: google domais)
- Possuir email (ex.: zoho)

Devera ser passado para o SES da aws o seu dominio e email que irao passar uma uma validacao, depois você deve buscar em detalhes do dominio inserido na AWs e setar em DNS no painel do seu dominio

2º config

Ainda dentro do painel da AWS, pesquise por "IAM" -> usuarios -> adicionar permissao -> anexar politicas existentes de forma direta -> *pesquisar por SeS  e adicionar a FullAccess marcando a caixa -> proximo -> adicionar.
