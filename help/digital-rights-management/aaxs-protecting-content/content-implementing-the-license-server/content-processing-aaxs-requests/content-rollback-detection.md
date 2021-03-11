---
title: Detecção de reversão
description: Detecção de reversão
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Detecção de reversão{#rollback-detection}

Para detecção de reversão, algumas regras de uso exigem que o cliente mantenha as informações de estado para a aplicação dos direitos. Por exemplo, para impor a regra de uso da janela de reprodução, o cliente armazena a data e a hora em que o usuário começou a visualizar o conteúdo pela primeira vez. Esse evento aciona o início da janela de reprodução. Para aplicar com segurança a janela de reprodução, o servidor precisa garantir que o usuário não esteja fazendo backup e restaurando o estado do cliente para remover o tempo de início da janela de reprodução armazenado no cliente. O servidor faz isso rastreando o valor do contador de reversão do cliente. Para cada solicitação, o servidor obtém o valor do contador ao chamar `RequestMessageBase.getClientState()` para obter o objeto `ClientState` e, em seguida, chamar `ClientState.getCounter()` para obter o valor atual do contador de estado do cliente. O servidor deve armazenar esse valor para cada cliente (use `MachineId.getUniqueId()` para identificar o cliente associado ao valor do contador de reversão) e, em seguida, chame `ClientState.incrementCounter()` para aumentar o valor do contador em um. Se o servidor detectar que o valor do contador é inferior ao último valor visto pelo servidor, o estado do cliente pode ter sido revertido. Para obter mais informações sobre a detecção de adulteração do estado do cliente, consulte a documentação de referência da API `ClientState` .
