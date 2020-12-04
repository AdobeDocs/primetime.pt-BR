---
seo-title: Tratamento de solicitações de sincronização
title: Tratamento de solicitações de sincronização
uuid: 37b2db09-4c09-4216-874b-b570a84569b6
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Tratamento de solicitações de sincronização{#handling-synchronization-requests}

. Se uma licença especificar os requisitos de sincronização ([Requisitos para sincronização](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization)), o cliente enviará periodicamente solicitações de sincronização ao servidor, com base na frequência especificada na licença. Para ativar mensagens de sincronização, defina SyncFrequencyRequirements em um PlayRight.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Se o protocolo de suporte do cliente e do servidor versão 5, o URL da solicitação será &quot;URL do servidor de licença nos metadados: + &quot;/flashaccess/sync/v4&quot;. Caso contrário, o URL da solicitação será &quot;URL do License Server em metadados&quot; + &quot;/flashaccess/sync/v3&quot;

As mensagens de sincronização são usadas para sincronizar o horário do cliente com o horário do servidor. Se as licenças estiverem incorporadas no conteúdo e não precisarem ser recuperadas de um servidor de licenças, a sincronização do tempo do cliente é importante para impedir que o cliente modifique seu relógio para evitar a expiração da licença.

As mensagens de sincronização também podem ser usadas para comunicar as informações de estado do cliente ao servidor ( `getClientState()`) para detecção de reversão. Consulte [Proteção de Reversão](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md).