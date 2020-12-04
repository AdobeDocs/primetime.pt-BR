---
seo-title: Detecção de retorno
title: Detecção de retorno
uuid: ec124bac-a1d7-45be-bf09-a99d5eec5042
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Detecção de reversão {#rollback-detection}

Para a detecção de reversão, algumas regras de uso exigem que o cliente mantenha informações de estado para a aplicação dos direitos. Por exemplo, para impor a regra de uso da janela de reprodução, o cliente armazena a data e a hora em que o usuário começou a exibir o conteúdo pela primeira vez. Este evento aciona o start da janela de reprodução. Para aplicar com segurança a janela de reprodução, o servidor precisa garantir que o usuário não esteja fazendo backup e restaurando o estado do cliente para remover o tempo de start da janela de reprodução armazenado no cliente. O servidor faz isso rastreando o valor do contador de reversão do cliente.

Para cada solicitação, o servidor obtém o valor do contador chamando `RequestMessageBase.getClientState()` para obter o objeto `ClientState` e, em seguida, chamando `ClientState.getCounter()` para obter o valor atual do contador de estado do cliente. O servidor deve armazenar esse valor para cada cliente (use `MachineId.getUniqueId()` para identificar o cliente associado ao valor do contador de rollback) e, em seguida, chame `ClientState.incrementCounter()` para aumentar o valor do contador em um. Se o servidor detectar que o valor do contador é menor que o último valor visto pelo servidor, o estado do cliente pode ter sido revertido.

Consulte a documentação de referência da API `ClientState` para obter mais informações sobre a detecção de adulteração do estado do cliente.
