---
title: Detecção de reversão
description: Detecção de reversão
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Detecção de reversão {#rollback-detection}

Para a detecção de reversão, algumas regras de uso exigem que o cliente mantenha informações de estado para aplicar os direitos. Por exemplo, para impor a regra de uso da janela de reprodução, o cliente armazena a data e a hora em que o usuário começou a visualizar o conteúdo pela primeira vez. Esse evento aciona o início da janela de reprodução. Para impor com segurança a janela de reprodução, o servidor precisa garantir que o usuário não esteja fazendo backup e restaurando o estado do cliente para remover a hora de início da janela de reprodução armazenada no cliente. O servidor faz isso rastreando o valor do contador de reversão do cliente.

Para cada solicitação, o servidor obtém o valor do contador chamando `RequestMessageBase.getClientState()` para obter a `ClientState` objeto e, em seguida, chamando `ClientState.getCounter()` para obter o valor atual do contador de estado do cliente. O servidor deve armazenar esse valor para cada cliente (use `MachineId.getUniqueId()` para identificar o cliente associado ao valor do contador de reversão) e, em seguida, chame `ClientState.incrementCounter()` para aumentar o valor do contador em um. Se o servidor detectar que o valor do contador é menor que o último valor visto pelo servidor, o estado do cliente pode ter sido revertido.

Consulte a `ClientState` Documentação de referência de API para obter mais informações sobre a detecção de violação do estado do cliente.
