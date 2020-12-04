---
seo-title: Processar solicitações de sincronização
title: Processar solicitações de sincronização
uuid: e2623afb-7a57-402d-a8a1-07bcf6324d41
translation-type: tm+mt
source-git-commit: eed2ed2512c2c462cd43637d83d80bf9a5c0d490
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# Processar solicitações de sincronização {#handle-synchronization-requests}

Se uma licença especificar os requisitos de sincronização [Requisitos para sincronização,](../../protecting-content/introduction/usage-rules/authentication/synchronization.md) o cliente envia periodicamente solicitações de sincronização ao servidor, com base na frequência especificada na licença. Para ativar mensagens de sincronização, defina `SyncFrequencyRequirements` em PlayRight.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Se o protocolo de suporte do cliente e do servidor versão 5, o URL da solicitação será &quot;URL do servidor de licença nos metadados: + &quot; [!DNL /flashaccess/sync/v4]&quot;. Caso contrário, o URL da solicitação será &quot;URL do License Server em metadados&quot; + &quot; [!DNL /flashaccess/sync/v3]&quot;

As mensagens de sincronização são usadas para sincronizar o horário do cliente com o horário do servidor. Se as licenças estiverem incorporadas no conteúdo e não precisarem ser recuperadas de um servidor de licenças, a sincronização do tempo do cliente é importante para impedir que o cliente modifique seu relógio para evitar a expiração da licença.

As mensagens de sincronização também podem ser usadas para comunicar as informações de estado do cliente ao servidor ( `getClientState()`) para detecção de reversão.

Consulte [Proteção de Reversão](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#rollback-detection).
