---
title: Lidar com solicitações de cancelamento de registro de domínio
description: Lidar com solicitações de cancelamento de registro de domínio
copied-description: true
exl-id: 14b97ba2-9344-4d84-8c52-f33126337454
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Lidar com solicitações de cancelamento de registro de domínio {#handle-domain-de-registration-requests}

Se o aplicativo cliente precisar deixar um domínio, ele chamará a variável `DRMManager.removeFromDeviceGroup()`API do ActionScript ou o `leaveLicenseDomain()` API do iOS para iniciar o processo de cancelamento de registro do domínio. O cancelamento do registro de domínio é um processo em duas fases. O cliente envia primeiro uma solicitação de visualização de cancelamento de registro. O servidor de domínio examina a solicitação e determina se o cliente tem permissão para deixar o domínio. Um erro pode ser retornado se o computador não fizer parte do domínio no momento. Após uma resposta bem-sucedida, o cliente exclui suas credenciais de domínio e as licenças emitidas para esse domínio. Em seguida, envia uma solicitação de cancelamento de registro.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Se tanto o cliente quanto o servidor suportam o protocolo versão 5, o URL da solicitação é &quot;Domain Server URL in metadata: + &quot; [!DNL /flashaccess/dereg/v4]&quot;. Caso contrário, o URL da solicitação será o URL do servidor do domínio nos metadados&quot; + &quot; [!DNL /flashaccess/dereg/v3]&quot;

Ao processar solicitações de cancelamento de registro de domínio, o servidor usa `getRequestPhase()` para determinar se o cliente está na fase de pré-visualização ou cancelamento de registro. Na fase de visualização, o servidor de domínio examina a solicitação e determina se o cliente tem permissão para deixar o domínio porque a solicitação pode ser negada; por exemplo, a solicitação pode ser negada se a máquina não fizer parte do domínio no momento. Na fase de cancelamento de registro, o servidor registra o fato de que a máquina deixou o domínio. O servidor é altamente recomendado para avaliar a mesma lógica na solicitação de visualização que na solicitação real de cancelamento do registro para minimizar a chance de falha da segunda fase.
