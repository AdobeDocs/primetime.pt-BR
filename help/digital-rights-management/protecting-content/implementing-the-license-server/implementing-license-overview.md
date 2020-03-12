---
seo-title: Visão geral do servidor de licenças
title: Visão geral do servidor de licenças
uuid: 8c62376b-b159-4297-9322-75d62947e84e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Visão geral {#license-server-overview}

Antes de poder emitir licenças para clientes, você deve implantar um servidor de licenças DRM do Adobe Primetime. O servidor de licenças usa o SDK do DRM Primetime para executar várias tarefas.

Para implementar um Servidor de Licenças:

* Processar solicitações de autenticação, se a autenticação de nome de usuário/senha for suportada.
* Processar solicitações de licença
* Processar solicitações Obter versão do servidor — Todos os servidores devem implementar suporte para esse tipo de solicitação.
* Processar solicitações de registro de domínio — necessário somente se estiver implementando um servidor de domínio.
* Processar solicitações de cancelamento de registro de domínio — necessário somente se estiver implementando um servidor de domínio.
* Sincronização do processo — Necessário somente se as licenças especificarem os requisitos de sincronização.

Além disso, o servidor precisa fornecer lógica comercial para autenticar usuários, determinar se eles estão autorizados a exibir conteúdo e, opcionalmente, rastrear o uso de licenças.

Consulte Referência *da API DRM do* Adobe Primetime para obter detalhes sobre a API do Java.
