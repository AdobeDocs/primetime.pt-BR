---
title: Lidar com solicitações de autenticação
description: Lidar com solicitações de autenticação
copied-description: true
exl-id: c1d46ec0-e053-4824-b3b1-20320e259fbe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Lidar com solicitações de autenticação{#handling-authentication-requests}

A variável `AuthenticationHandler` é usada para processar solicitações de autenticação. Ele é usado apenas para autenticação de nome de usuário/senha.

Ao gerar o token de autenticação, a data de expiração do token deve ser especificada. As propriedades personalizadas também podem ser incluídas no token. Se definidas, essas propriedades estarão visíveis para o servidor quando o token de autenticação for enviado em solicitações subsequentes. Consulte [Lidar com solicitações de licença](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-handling-license-reqs.md) para obter informações sobre como manipular tokens de autenticação personalizados.

O manipulador lê uma solicitação de autenticação e analisa a mensagem de solicitação quando `parseRequest()` é chamado. A implementação do servidor examina as credenciais do usuário na solicitação e, se as credenciais forem válidas, gera um `AuthenticationToken` ao chamar `getRequest().generateAuthToken()`. Se `AuthenticationRequestMessage.generateAuthToken()` não é chamado antes de `close()`, um código de erro de falha de autenticação é enviado.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Se tanto o cliente quanto o servidor suportam o protocolo versão 5, o URL da solicitação é &quot;License Server URL in metadata: + &quot;/flashaccess/authn/v4&quot;. Se a versão 3 do protocolo for o máximo suportado pelo cliente ou servidor, os clientes do Adobe Access enviarão solicitações de autenticação para &quot;URL do License Server nos metadados&quot; + &quot;/flashaccess/authn/v3&quot;. Caso contrário, as solicitações de autenticação serão enviadas para &quot;URL do servidor de licenças nos metadados&quot; + &quot;/flashaccess/authn/v1&quot;
