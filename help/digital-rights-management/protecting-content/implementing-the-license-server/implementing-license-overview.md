---
title: Visão geral do servidor de licenças
description: Visão geral do servidor de licenças
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Visão geral {#license-server-overview}

Antes de poder emitir licenças para clientes, você deve implantar um servidor de licenças Adobe Primetime DRM. O servidor de licenças usa o SDK de DRM do Primetime para executar várias tarefas.

Para implementar um Servidor de Licenças:

* Processar solicitações de autenticação, se a autenticação de nome de usuário/senha for suportada.
* Processar solicitações de licença
* Processar Solicitações de Obtenção de Versão do Servidor — Todos os servidores devem implementar o suporte para esse tipo de solicitação.
* Processar solicitações de registro de domínio — necessário somente se estiver implementando um servidor de domínio.
* Processar solicitações de cancelamento de registro do domínio — necessário somente se estiver implementando um servidor de domínio.
* Sincronização de processos — Necessária somente se as licenças especificarem os requisitos de sincronização.

Além disso, o servidor precisa fornecer lógica de negócios para autenticar usuários, determinar se os usuários estão autorizados a exibir conteúdo e, opcionalmente, rastrear o uso da licença.

Consulte *Referência da API DRM do Adobe Primetime* para obter detalhes sobre a API do Java.
