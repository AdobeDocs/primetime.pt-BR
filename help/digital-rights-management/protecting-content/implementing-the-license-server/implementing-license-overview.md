---
title: Visão geral do servidor de licenças
description: Visão geral do servidor de licenças
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Visão geral {#license-server-overview}

Antes de emitir licenças para clientes, é necessário implantar um servidor de licenças do Adobe Primetime DRM. O servidor de licença usa o SDK DRM do Primetime para executar várias tarefas.

Para implementar um Servidor de Licenças:

* Processar solicitações de autenticação, se a autenticação de nome de usuário/senha for suportada.
* Processar solicitações de licença
* Processar Solicitações de Obtenção de Versão do Servidor — Todos os servidores devem implementar o suporte para esse tipo de solicitação.
* Processar solicitações de registro de domínio — Necessário apenas se estiver implementando um servidor de domínio.
* Processar solicitações de cancelamento de registro de domínio — necessário apenas se estiver implementando um servidor de domínio.
* Sincronização de processos — necessária somente se as licenças especificarem requisitos de sincronização.

Além disso, o servidor precisa fornecer uma lógica de negócios para autenticar usuários, determinar se os usuários estão autorizados a visualizar conteúdo e, opcionalmente, rastrear o uso da licença.

Consulte *Referência da API do Adobe Primetime DRM* para obter detalhes sobre a API do Java.
