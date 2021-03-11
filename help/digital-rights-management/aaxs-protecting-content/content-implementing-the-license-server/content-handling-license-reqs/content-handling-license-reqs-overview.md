---
title: Visão geral
description: Visão geral
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Visão geral{#overview}

Para solicitar uma licença, o cliente envia os metadados que foram incorporados no conteúdo durante a embalagem. O servidor de licenças usa as informações nos metadados de conteúdo para gerar uma licença.

O `LicenseHandler` lê uma solicitação de licença e analisa a solicitação. `LicenseHandler`O se estende  `BatchHandlerBase` para acomodar solicitações de licença em lote, embora esse recurso não seja suportado atualmente pelos clientes do Adobe Access. O método `getRequests()` retornará uma Lista de objetos `LicenseRequestMessage`. O chamador deve repetir o `LicenseRequestMessages` e, para cada solicitação, gerar uma licença ou definir um código de erro (consulte a documentação de referência da API `LicenseRequestMessage` para obter detalhes). Para cada solicitação de licença, o servidor determina se emitirá uma licença. Chame `LicenseRequestMessage.getContentInfo()` para obter informações extraídas dos metadados do conteúdo, incluindo a ID de conteúdo, a ID de licença e as políticas.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* A classe da mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* Se o cliente e o servidor tiverem suporte para a versão 5 do protocolo, o URL da solicitação será &quot;URL do servidor de licença em metadados: + &quot;/flashaccess/license/v4&quot;. Se a versão 3 do protocolo for o máximo suportado pelo cliente ou servidor, os clientes do Adobe Access enviarão solicitações de autenticação para &quot;URL do License Server em metadados&quot; + &quot;/flashaccess/license/v3&quot;. Caso contrário, as solicitações de autenticação serão enviadas para &quot;URL do License Server em metadados&quot; + &quot;/flashaccess/license/v1&quot;

Se ocorrer um erro ao analisar a solicitação, um `HandlerParsingException` será lançado. Esta exceção contém informações de erro a serem retornadas ao cliente. Para recuperar as informações do erro, chame `HandlerParsingException.getErrorData()`. Se ocorrer um erro ao gerar uma licença porque os requisitos de política não foram cumpridos, um `PolicyEvaluationException` será lançado. Essa exceção também inclui `ErrorData` para ser retornado ao cliente. Consulte a documentação da API para `LicenseRequestMessage.generateLicense()` para obter detalhes sobre como as políticas são avaliadas durante a geração de licenças.

As licenças e erros são enviados ao mesmo tempo em que `LicenseHandler.close()` é chamado.

Um dispositivo pode ter várias licenças para o mesmo conteúdo (mesma ID de licença), mas só pode ter uma licença para uma ID de licença e ID de política específicos. Se receber uma licença com uma ID de Licença/ID de Política duplicada, a nova licença substituirá a antiga somente se a data de emissão da nova licença for posterior à data de emissão da licença existente. Essa lógica é usada para processar licenças incorporadas ao conteúdo, portanto, não é recomendável incorporar mais de uma licença com a mesma ID de política em um pedaço de conteúdo. A mesma lógica se aplica às licenças passadas para o cliente por meio da API `DRMManager.storeVoucher()` ActionScript3; se o cliente já possuir uma licença com data de emissão posterior, a licença fornecida pode ser ignorada.
