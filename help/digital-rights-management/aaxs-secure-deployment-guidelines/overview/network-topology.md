---
title: Visão geral da topologia de rede
description: Visão geral da topologia de rede
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Visão geral da topologia de rede {#network-topology-overview}

Depois de implantar o Adobe Access com êxito, é importante manter a segurança do ambiente. Esta seção descreve as tarefas necessárias para manter a segurança do servidor de produção do Adobe Access.

Use um *proxy reverso* para garantir que diferentes conjuntos de URLs para aplicativos Web de Adobe Access estejam disponíveis para usuários externos e internos. Essa configuração é mais segura do que permitir que os usuários se conectem diretamente ao servidor de aplicativos no qual o Adobe Access está sendo executado. O proxy reverso executa todas as solicitações HTTP para o servidor de aplicativos que está executando o Adobe Access. Os usuários só têm acesso de rede ao proxy reverso e podem tentar apenas as conexões de URL compatíveis com o proxy reverso.

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)

