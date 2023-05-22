---
title: Visão geral da topologia de rede
description: Visão geral da topologia de rede
copied-description: true
exl-id: ca5e8701-f8a3-4125-bb60-bfb9efd5c8f3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---

# Visão geral da topologia de rede {#network-topology-overview}

Depois de implantar o Acesso ao Adobe com êxito, é importante manter a segurança do ambiente. Esta seção descreve as tarefas necessárias para manter a segurança do servidor de produção de Acesso ao Adobe.

Use um *proxy reverso* para garantir que diferentes conjuntos de URLs para aplicativos web de acesso ao Adobe estejam disponíveis para usuários externos e internos. Essa configuração é mais segura do que permitir que os usuários se conectem diretamente ao servidor de aplicativos no qual o Adobe Access está sendo executado. O proxy reverso executa todas as solicitações HTTP para o servidor de aplicativos que está executando o Acesso ao Adobe. Os usuários só têm acesso de rede ao proxy reverso e podem tentar apenas as conexões de URL compatíveis com o proxy reverso.

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)
