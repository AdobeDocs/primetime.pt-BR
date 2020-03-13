---
seo-title: Visão geral
title: Visão geral
uuid: d3bfa65b-2360-4843-b59e-71451fa62a2c
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Visão geral{#overview}

Para solicitar uma licença, o cliente envia os metadados que foram incorporados no conteúdo durante o empacotamento. O servidor de licenças usa as informações nos metadados do conteúdo para gerar uma licença.

O usuário `LicenseHandler` lê uma solicitação de licença e analisa a solicitação. `LicenseHandler`se estende `BatchHandlerBase` para acomodar solicitações de licença em lote, embora esse recurso não seja suportado atualmente pelos clientes do Adobe Access. O `getRequests()` método retornará uma Lista de `LicenseRequestMessage` objetos. O chamador deve repetir o processo e, para cada solicitação, gerar uma licença ou definir um código de erro (consulte a documentação de referência da `LicenseRequestMessages``LicenseRequestMessage` API para obter detalhes). Para cada solicitação de licença, o servidor determina se ele emitirá uma licença. Chame `LicenseRequestMessage.getContentInfo()` para obter informações extraídas dos metadados do conteúdo, incluindo a ID do conteúdo, a ID da licença e as políticas.

* A classe do manipulador de solicitação é `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* Se o protocolo de suporte do cliente e do servidor versão 5, o URL da solicitação será &quot;URL do servidor de licença nos metadados: + &quot;/flashaccess/license/v4&quot;. Se a versão 3 do protocolo for o máximo suportado pelo cliente ou servidor, os clientes do Adobe Access enviarão solicitações de autenticação para &quot;URL do License Server em metadados&quot; + &quot;/flashaccess/license/v3&quot;. Caso contrário, as solicitações de autenticação serão enviadas para &quot;URL do License Server em metadados&quot; + &quot;/flashaccess/license/v1&quot;

Se ocorrer um erro ao analisar a solicitação, um erro `HandlerParsingException` será lançado. Esta exceção contém informações de erro a serem retornadas ao cliente. Para recuperar as informações do erro, chame `HandlerParsingException.getErrorData()`. Se ocorrer um erro ao gerar uma licença porque os requisitos de política não foram atendidos, um erro será lançado `PolicyEvaluationException` . Essa exceção também inclui `ErrorData` o retorno para o cliente. Consulte a documentação da API para obter detalhes `LicenseRequestMessage.generateLicense()` sobre como as políticas são avaliadas durante a geração da licença.

As licenças e os erros são enviados ao mesmo tempo em que `LicenseHandler.close()` são chamados.

Um dispositivo pode ter várias licenças para o mesmo conteúdo (mesma ID de licença), mas só pode ter uma licença para uma determinada ID de licença e ID de política. Se receber uma licença com uma ID de Licença/ID de Política duplicada, a nova licença substituirá a antiga somente se a data de emissão da nova licença for posterior à data de emissão da licença existente. Essa lógica é usada para processar licenças incorporadas ao conteúdo, portanto, não é recomendável incorporar mais de uma licença com a mesma ID de política em uma parte do conteúdo. A mesma lógica se aplica às licenças enviadas para o cliente por meio da API do `DRMManager.storeVoucher()` ActionScript3; se o cliente já possuir uma licença com data de emissão posterior, a licença fornecida poderá ser ignorada.
