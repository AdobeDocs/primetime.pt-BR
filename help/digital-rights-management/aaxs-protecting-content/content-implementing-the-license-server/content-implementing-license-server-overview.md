---
seo-title: Visão geral
title: Visão geral
uuid: f4ae10ca-6e2a-4313-80a0-4c7377dba000
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Visão geral{#overview}

Para emitir licenças para clientes, você deve implantar um servidor de licenças de Adobe Access. O servidor de licenças usa o SDK do Adobe® Access™ para executar estas tarefas:

* Processar solicitações de autenticação, se a autenticação de nome de usuário/senha for suportada.
* Processar solicitações de licença
* Processar solicitações Get Server Version — Todos os servidores devem implementar suporte para esse tipo de solicitação.
* Processar solicitações de registro de domínio — necessário somente se estiver implementando um servidor de domínio.
* Processar solicitações de cancelamento de registro de domínio — necessário somente se estiver implementando um servidor de domínio.
* Sincronização de processos — Necessário somente se as licenças especificarem os requisitos de sincronização.

Além disso, o servidor precisa fornecer lógica comercial para autenticar usuários, determinar se eles estão autorizados a visualização de conteúdo e, opcionalmente, rastrear o uso de licenças.

Para obter detalhes sobre a API Java discutida neste capítulo, consulte *Referência da API de acesso ao Adobe*.
