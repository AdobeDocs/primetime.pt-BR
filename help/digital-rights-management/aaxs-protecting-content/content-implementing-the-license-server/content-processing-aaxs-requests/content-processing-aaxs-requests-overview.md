---
title: Visão geral
description: Visão geral
copied-description: true
exl-id: d284b279-d261-4573-825d-919a551b3194
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Visão geral{#overview}

A abordagem geral para lidar com solicitações é criar um manipulador, analisar a solicitação, definir os dados de resposta ou o código de erro e fechar o manipulador.

A classe base usada para lidar com uma única interação de solicitação/resposta é `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Uma instância do `HandlerConfiguration` é usada para inicializar o manipulador. `HandlerConfiguration` armazena informações de configuração do servidor, incluindo credenciais de transporte, tolerância de carimbo de data e hora, listas de atualização de política e listas de revogação. O manipulador lê os dados da solicitação e analisa a solicitação em uma instância de `RequestMessageBase`. O chamador pode examinar as informações na solicitação e decidir se retorna um erro ou uma resposta bem-sucedida (subclasses de `RequestMessageBase` forneça um método para definir os dados de resposta).

Se a solicitação for bem-sucedida, defina os dados de resposta; caso contrário, chame `RequestMessageBase.setErrorData()` em caso de falha. Sempre encerre a implementação invocando o `close()` (recomenda-se que `close()` ser chamado no `finally` bloco de um `try` declaração). Consulte a `MessageHandlerBase` Documentação de referência de API para obter um exemplo de como chamar o manipulador.

>[!NOTE]
>
>O código de status HTTP 200 (OK) deve ser enviado em resposta a todas as solicitações processadas pelo manipulador. Se o manipulador não pôde ser criado devido a um erro do servidor, o servidor pode responder com outro código de status, como 500 (Erro interno do servidor).

O cliente usa o URL do License Server especificado no momento do empacotamento como o URL base para todas as solicitações enviadas ao servidor de licenças. Por exemplo, se o URL do servidor for especificado como &quot;ht<span></span>tps://licenseserver.com/path&quot;, o cliente enviará solicitações para &quot;ht<span></span>tps://licenseserver.com/path/flashaccess/...&quot;. Consulte as seções a seguir para obter detalhes sobre o caminho específico usado para cada tipo de solicitação. Ao implementar seu servidor de licenças, certifique-se de que o servidor responde aos caminhos necessários para cada tipo de solicitação.

Uma solicitação de licença pode conter um token de autenticação. Se uma autenticação de nome de usuário/senha foi usada, a solicitação pode conter uma `AuthenticationToken` gerado pelo `AuthenticationHandler`, e o SDK garantirá que o token seja válido antes de emitir uma licença.
