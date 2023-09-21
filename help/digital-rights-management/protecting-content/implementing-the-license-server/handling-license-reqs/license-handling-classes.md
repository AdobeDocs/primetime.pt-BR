---
title: Visão geral
description: Visão geral
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Visão geral {#overview}

Para obter uma licença, os clientes formam uma solicitação dos metadados incorporados ao conteúdo empacotado e, em seguida, enviam essa solicitação ao servidor de licenças. O servidor de licença usa informações extraídas dos metadados do conteúdo para gerar uma licença.

Se o cliente e o servidor suportarem a versão 5 do protocolo, o URL da solicitação será &quot;URL do servidor de licenças nos metadados&quot; + &quot; [!DNL /flashaccess/license/v4]&quot;. Se a versão 3 do protocolo for o máximo suportado pelo cliente ou servidor, os clientes DRM Primetime enviarão solicitações de autenticação para &quot;URL do servidor de licenças nos metadados&quot; + &quot; [!DNL /flashaccess/license/v3]&quot;. Caso contrário, as solicitações de autenticação serão enviadas para &quot;URL do servidor de licenças nos metadados&quot; + &quot; [!DNL /flashaccess/license/v1]&quot;

Um dispositivo pode ter várias licenças para o mesmo conteúdo (mesma ID de licença), mas só pode ter uma licença para uma ID de licença e ID de política DRM específicas. Se ele receber uma licença com uma ID de licença/ID de política duplicada, a nova licença substituirá a antiga somente se a data de emissão da nova licença for posterior à data de emissão da licença existente. Essa lógica é usada para processar licenças incorporadas ao conteúdo. Portanto, não é recomendável incorporar mais de uma licença com a mesma ID de política de DRM em uma parte do conteúdo. A mesma lógica se aplica às licenças passadas para o cliente por meio do `DRMManager.storeVoucher()` API do ActionScript3; se o cliente já possuir uma licença com uma data de emissão posterior, a licença fornecida poderá ser ignorada.

## Classes de manipulação de solicitação de licença {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` - Esta é a classe do manipulador de solicitação de licença. Ele lê e analisa solicitações de licença. Seus `getRequests()` O método retorna uma lista de `LicenseRequestMessage` objetos.
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` - Esta é a classe de mensagem de solicitação. O chamador deve iterar através da variável `LicenseRequestMessage` lista retornada por `getRequests()`e para cada solicitação gere uma licença ou defina um código de erro. Chame `LicenseRequestMessage.getContentInfo()` para obter informações extraídas dos metadados do conteúdo, incluindo as políticas de ID de conteúdo, ID de licença e DRM.

As licenças e os erros são enviados ao mesmo tempo em que a `LicenseHandler.close()` é chamado.

Consulte a [Documentação de referência da API do servidor DRM](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) para obter detalhes.
