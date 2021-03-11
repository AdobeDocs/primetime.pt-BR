---
title: Tratamento de solicitações de autenticação
description: Tratamento de solicitações de autenticação
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Lidar com solicitações de autenticação{#handling-authentication-requests}

A classe `AuthenticationHandler` é usada para processar solicitações de autenticação. Ele é usado somente para autenticação de nome de usuário/senha.

Ao gerar o token de autenticação, a data de expiração do token deve ser especificada. Propriedades personalizadas também podem ser incluídas no token. Se definidas, essas propriedades ficarão visíveis para o servidor quando o token de autenticação for enviado em solicitações subsequentes. Consulte [Manipulação de solicitações de licença](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-handling-license-reqs.md) para obter informações sobre como lidar com tokens de autenticação personalizados.

O manipulador lê uma solicitação de autenticação e analisa a mensagem da solicitação quando `parseRequest()` é chamado. A implementação do servidor examina as credenciais do usuário na solicitação e, se as credenciais forem válidas, gera um objeto `AuthenticationToken` chamando `getRequest().generateAuthToken()`. Se `AuthenticationRequestMessage.generateAuthToken()` não for chamado antes de `close()`, um código de erro de falha de autenticação será enviado.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* A classe da mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Se o cliente e o servidor tiverem suporte para a versão 5 do protocolo, o URL da solicitação será &quot;URL do servidor de licença em metadados: + &quot;/flashaccess/authn/v4&quot;. Se a versão 3 do protocolo for o máximo suportado pelo cliente ou servidor, os clientes do Adobe Access enviarão solicitações de autenticação para &quot;URL do License Server em metadados&quot; + &quot;/flashaccess/authn/v3&quot;. Caso contrário, as solicitações de autenticação serão enviadas para &quot;URL do License Server em metadados&quot; + &quot;/flashaccess/authn/v1&quot;

