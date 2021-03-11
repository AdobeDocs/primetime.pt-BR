---
title: Gerenciar solicitações de sincronização
description: Gerenciar solicitações de sincronização
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# Gerenciar solicitações de sincronização {#handle-synchronization-requests}

Se uma licença especificar requisitos de sincronização [Requisitos para Sincronização,](../../protecting-content/introduction/usage-rules/authentication/synchronization.md) o cliente envia periodicamente solicitações de sincronização para o servidor, com base na frequência especificada na licença. Para ativar mensagens de sincronização, defina `SyncFrequencyRequirements` em PlayRight.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* A classe da mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Se o cliente e o servidor tiverem suporte para a versão 5 do protocolo, o URL da solicitação será &quot;URL do servidor de licença em metadados: + &quot; [!DNL /flashaccess/sync/v4]&quot;. Caso contrário, o URL da solicitação será &quot;URL do License Server em metadados&quot; + &quot; [!DNL /flashaccess/sync/v3]&quot;

As mensagens de sincronização são usadas para sincronizar o horário do cliente com o horário do servidor. Se as licenças estiverem incorporadas no conteúdo e não precisarem ser recuperadas de um servidor de licenças, sincronizar o tempo do cliente é importante para impedir que o cliente modifique seu relógio para ignorar a expiração da licença.

As mensagens de sincronização também podem ser usadas para comunicar as informações de estado do cliente ao servidor ( `getClientState()`) para detecção de rollback.

Consulte [Proteção de Reversão](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#rollback-detection).
