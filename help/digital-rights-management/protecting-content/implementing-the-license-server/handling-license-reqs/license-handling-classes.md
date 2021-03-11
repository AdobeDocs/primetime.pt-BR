---
title: Visão geral
description: Visão geral
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Visão geral {#overview}

Para obter uma licença, os clientes formam uma solicitação dos metadados incorporados no conteúdo empacotado e, em seguida, enviam essa solicitação ao servidor de licença. O servidor de licenças usa informações extraídas dos metadados de conteúdo para gerar uma licença.

Se o cliente e o servidor oferecerem suporte à versão 5 do protocolo, o URL da solicitação será &quot;URL do License Server em metadados&quot; + &quot; [!DNL /flashaccess/license/v4]&quot;. Se a versão 3 do protocolo for o máximo suportado pelo cliente ou servidor, os clientes DRM do Primetime enviarão solicitações de autenticação para &quot;URL do License Server em metadados&quot; + &quot; [!DNL /flashaccess/license/v3]&quot;. Caso contrário, as solicitações de autenticação serão enviadas para &quot;URL do License Server em metadados&quot; + &quot; [!DNL /flashaccess/license/v1]&quot;

Um dispositivo pode ter várias licenças para o mesmo conteúdo (mesma ID de licença), mas só pode ter uma licença para uma ID de licença específica e ID de política de DRM. Se receber uma licença com uma ID de Licença/ID de Política duplicada, a nova licença substituirá a antiga somente se a data de emissão da nova licença for posterior à data de emissão da licença existente. Essa lógica é usada para processar licenças incorporadas ao conteúdo. Portanto, não é recomendável incorporar mais de uma licença com a mesma ID de política de DRM em uma parte do conteúdo. A mesma lógica se aplica às licenças passadas para o cliente por meio da API `DRMManager.storeVoucher()` ActionScript3; se o cliente já possuir uma licença com data de emissão posterior, a licença fornecida pode ser ignorada.

## Classes de tratamento de solicitação de licença {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` - Esta é a classe do manipulador de solicitação de licença. Ele lê e analisa solicitações de licença. Seu método `getRequests()` retorna uma lista de objetos `LicenseRequestMessage`.
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` - Esta é a classe de mensagem de solicitação. O chamador deve percorrer a lista `LicenseRequestMessage` retornada por `getRequests()` e, para cada solicitação, gerar uma licença ou definir um código de erro. Chame `LicenseRequestMessage.getContentInfo()` para obter informações extraídas dos metadados de conteúdo, incluindo a ID de conteúdo, a ID de licença e as políticas de DRM.

As licenças e erros são enviados de uma vez quando o método `LicenseHandler.close()` é chamado.

Consulte a [documentação de referência da API do servidor DRM](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) para obter detalhes.
