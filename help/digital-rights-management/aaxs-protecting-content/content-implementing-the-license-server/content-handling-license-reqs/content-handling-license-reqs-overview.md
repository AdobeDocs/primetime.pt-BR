---
title: Visão geral
description: Visão geral
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Visão geral{#overview}

Para solicitar uma licença, o cliente envia os metadados que foram incorporados ao conteúdo durante o empacotamento. O servidor de licenças usa as informações nos metadados de conteúdo para gerar uma licença.

A variável `LicenseHandler` O lê uma solicitação de licença e analisa a solicitação. `LicenseHandler`estende `BatchHandlerBase` para acomodar solicitações de licença em lote, embora no momento esse recurso não seja suportado pelos clientes do Adobe Access. A variável `getRequests()` retornará uma Lista de `LicenseRequestMessage` objetos. O chamador deve iterar através da variável `LicenseRequestMessages`e para cada solicitação, gere uma licença ou defina um código de erro (consulte `LicenseRequestMessage` Documentação de referência da API para obter detalhes). Para cada solicitação de licença, o servidor determina se emitirá uma licença. Chame `LicenseRequestMessage.getContentInfo()` para obter informações extraídas dos metadados do conteúdo, incluindo a ID do conteúdo, a ID da licença e as políticas.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* Se tanto o cliente quanto o servidor suportam o protocolo versão 5, o URL da solicitação é &quot;License Server URL in metadata: + &quot;/flashaccess/license/v4&quot;. Se a versão 3 do protocolo for o máximo suportado pelo cliente ou servidor, os clientes do Adobe Access enviarão solicitações de autenticação para &quot;URL do License Server nos metadados&quot; + &quot;/flashaccess/license/v3&quot;. Caso contrário, as solicitações de autenticação serão enviadas para &quot;URL do servidor de licenças nos metadados&quot; + &quot;/flashaccess/license/v1&quot;

Se ocorrer um erro ao analisar a solicitação, uma solicitação `HandlerParsingException` é lançado. Esta exceção contém informações de erro a serem retornadas ao cliente. Para recuperar as informações do erro, chame `HandlerParsingException.getErrorData()`. Se ocorrer um erro durante a geração de uma licença porque os requisitos da política não foram atendidos, uma `PolicyEvaluationException` é lançado. Esta exceção também inclui `ErrorData` para ser devolvido ao cliente. Consulte a documentação da API para `LicenseRequestMessage.generateLicense()` para obter detalhes sobre como as políticas são avaliadas durante a geração da licença.

As licenças e os erros são enviados simultaneamente quando `LicenseHandler.close()` é chamado.

Um dispositivo pode ter várias licenças para o mesmo conteúdo (mesma ID de licença), mas só pode ter uma licença para uma ID de licença e ID de política específicas. Se ele receber uma licença com uma ID de licença/ID de política duplicada, a nova licença substituirá a antiga somente se a data de emissão da nova licença for posterior à data de emissão da licença existente. Essa lógica é usada para processar licenças incorporadas ao conteúdo, portanto, não é recomendável incorporar mais de uma licença com a mesma ID de política em uma parte do conteúdo. A mesma lógica se aplica às licenças passadas para o cliente por meio do `DRMManager.storeVoucher()` API do ActionScript3; se o cliente já possuir uma licença com uma data de emissão posterior, a licença fornecida poderá ser ignorada.
