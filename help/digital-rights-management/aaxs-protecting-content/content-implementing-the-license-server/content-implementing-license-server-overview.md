---
title: Visão geral
description: Visão geral
copied-description: true
exl-id: 7327386b-e796-4fa5-bda4-cacc612a9d1f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Visão geral{#overview}

Para emitir licenças aos clientes, você deve implantar um servidor de licenças de Acesso ao Adobe. O servidor de licenças usa o SDK do Adobe® Access™ para executar estas tarefas:

* Processar solicitações de autenticação, se a autenticação de nome de usuário/senha for suportada.
* Processar solicitações de licença
* Processar Solicitações de Obtenção de Versão do Servidor — Todos os servidores devem implementar o suporte para esse tipo de solicitação.
* Processar solicitações de registro de domínio — Necessário apenas se estiver implementando um servidor de domínio.
* Processar solicitações de cancelamento de registro de domínio — necessário apenas se estiver implementando um servidor de domínio.
* Sincronização de processos — necessária somente se as licenças especificarem requisitos de sincronização.

Além disso, o servidor precisa fornecer uma lógica de negócios para autenticar usuários, determinar se os usuários estão autorizados a visualizar conteúdo e, opcionalmente, rastrear o uso da licença.

Para obter detalhes sobre a API Java discutida neste capítulo, consulte *Referência da API de acesso do Adobe*.
