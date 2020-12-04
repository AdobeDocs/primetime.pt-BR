---
seo-title: Tratamento de solicitações de cancelamento de registro de domínio
title: Tratamento de solicitações de cancelamento de registro de domínio
uuid: 6f056b2b-374d-4e4d-926a-68605b2c923b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Tratamento de solicitações de cancelamento de registro do domínio{#handling-domain-de-registration-requests}

Se o aplicativo cliente precisar sair de um domínio, ele chamará a `DRMManager.removeFromDeviceGroup()`API do ActionScript ou a `leaveLicenseDomain()` API do iOS para iniciar o processo de cancelamento de registro do domínio. O cancelamento do registro do domínio é um processo de duas fases. O cliente envia primeiro uma solicitação de pré-visualização de cancelamento de registro. O servidor de domínio examina a solicitação e determina se o cliente pode sair do domínio (um erro pode ser retornado se o computador não fizer parte do domínio). Após uma resposta bem-sucedida, o cliente exclui suas credenciais de domínio e quaisquer licenças emitidas para esse domínio e, em seguida, envia uma solicitação de cancelamento de registro.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Se o protocolo de suporte do cliente e do servidor versão 5, o URL da solicitação será &quot;URL do servidor de domínio nos metadados: + &quot;/flashaccess/dereg/v4&quot;. Caso contrário, o URL da solicitação será o URL do Servidor de Domínio nos metadados&quot; + &quot;/flashaccess/dereg/v3&quot;

Ao processar solicitações de cancelamento de registro de domínio, o servidor usa `getRequestPhase()` para determinar se o cliente está na fase de pré-visualização ou cancelamento de registro. Na fase de pré-visualização, o servidor de domínio examina a solicitação e determina se o cliente pode sair do domínio (a solicitação pode ser negada, por exemplo, se o computador não fizer parte do domínio no momento). Na fase de cancelamento de registro, o servidor registra o fato de a máquina ter deixado o domínio. É altamente recomendável que o servidor avalie a mesma lógica na solicitação de pré-visualização como na solicitação de cancelamento de registro real para minimizar a chance da segunda fase falhar.
