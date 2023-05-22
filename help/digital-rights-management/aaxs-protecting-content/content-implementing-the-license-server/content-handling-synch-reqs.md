---
title: Lidar com solicitações de sincronização
description: Lidar com solicitações de sincronização
copied-description: true
exl-id: bbfc6096-72df-4597-96b3-8f67a640ea8f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Lidar com solicitações de sincronização{#handling-synchronization-requests}

. Se uma licença especificar requisitos de sincronização ([Requisitos para sincronização](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization)), o cliente enviará periodicamente solicitações de sincronização ao servidor, com base na frequência especificada na licença. Para habilitar mensagens de sincronização, defina SyncFrequencyRequirements em um PlayRight.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Se tanto o cliente quanto o servidor suportam o protocolo versão 5, o URL da solicitação é &quot;License Server URL in metadata: + &quot;/flashaccess/sync/v4&quot;. Caso contrário, o URL da solicitação será &quot;URL do servidor de licenças nos metadados&quot; + &quot;/flashaccess/sync/v3&quot;

As mensagens de sincronização são usadas para sincronizar o horário do cliente com o horário do servidor. Se as licenças estiverem incorporadas ao conteúdo e não precisarem ser recuperadas de um servidor de licenças, a sincronização do horário do cliente é importante para impedir que o cliente modifique o relógio para ignorar a expiração da licença.

As mensagens de sincronização também podem ser usadas para comunicar as informações de estado do cliente ao servidor ( `getClientState()`) para detecção de reversão. Consulte [Proteção de reversão](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md).
