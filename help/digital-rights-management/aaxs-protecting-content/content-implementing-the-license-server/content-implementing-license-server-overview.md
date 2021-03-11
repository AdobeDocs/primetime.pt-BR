---
title: Visão geral
description: Visão geral
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Visão geral{#overview}

Para emitir licenças para clientes, você deve implantar um servidor de licenças Adobe Access. O servidor de licenças usa o SDK do Adobe® Access™ para executar estas tarefas:

* Processar solicitações de autenticação, se a autenticação de nome de usuário/senha for suportada.
* Processar solicitações de licença
* Processar Solicitações de Obtenção de Versão do Servidor — Todos os servidores devem implementar o suporte para esse tipo de solicitação.
* Processar solicitações de registro de domínio — Necessário somente se estiver implementando um servidor de domínio.
* Processar solicitações de cancelamento de registro do domínio — necessário somente se estiver implementando um servidor de domínio.
* Sincronização de processos — Necessária somente se as licenças especificarem os requisitos de sincronização.

Além disso, o servidor precisa fornecer lógica de negócios para autenticar usuários, determinar se os usuários estão autorizados a exibir conteúdo e, opcionalmente, rastrear o uso da licença.

Para obter detalhes sobre a API do Java discutida neste capítulo, consulte *Referência da API de acesso ao Adobe*.
