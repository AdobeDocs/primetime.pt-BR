---
title: Gerenciar solicitações de cancelamento de registro do domínio
description: Gerenciar solicitações de cancelamento de registro do domínio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Gerenciar solicitações de cancelamento de registro do domínio {#handle-domain-de-registration-requests}

Se o aplicativo cliente precisar deixar um domínio, ele chamará a `DRMManager.removeFromDeviceGroup()`API do ActionScript ou a `leaveLicenseDomain()` API do iOS para iniciar o processo de cancelamento de registro do domínio. O cancelamento de registro do domínio é um processo de duas fases. Primeiro, o cliente envia uma solicitação de pré-visualização de cancelamento de registro. O servidor de domínio examina a solicitação e determina se o cliente tem permissão para sair do domínio. Um erro pode ser retornado se o computador não fizer parte do domínio no momento. Após uma resposta bem-sucedida, o cliente exclui suas credenciais de domínio e quaisquer licenças emitidas para esse domínio. Em seguida, envia uma solicitação de cancelamento de registro.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* A classe da mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Se o cliente e o servidor tiverem suporte para a versão 5 do protocolo, o URL da solicitação será &quot;URL do servidor de domínio nos metadados: + &quot; [!DNL /flashaccess/dereg/v4]&quot;. Caso contrário, o URL da solicitação será o URL do servidor de domínio nos metadados&quot; + &quot; [!DNL /flashaccess/dereg/v3]&quot;

Ao processar solicitações de cancelamento de registro do domínio, o servidor usa `getRequestPhase()` para determinar se o cliente está na fase de pré-visualização ou cancelamento de registro. Na fase de pré-visualização, o servidor de domínio examina a solicitação e determina se o cliente pode deixar o domínio porque a solicitação pode ser negada; por exemplo, a solicitação pode ser negada se o computador não fizer parte do domínio no momento. Na fase de cancelamento de registro, o servidor registra o fato de que a máquina deixou o domínio. O servidor é altamente recomendado para avaliar a mesma lógica na solicitação de visualização como na solicitação de cancelamento de registro real, para minimizar a chance de a segunda fase falhar.
