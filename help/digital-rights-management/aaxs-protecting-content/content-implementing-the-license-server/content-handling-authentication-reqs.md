---
seo-title: Tratamento de solicitações de autenticação
title: Tratamento de solicitações de autenticação
uuid: 036582d4-611c-4772-b247-81a3144fd5d6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Tratamento de solicitações de autenticação{#handling-authentication-requests}

A `AuthenticationHandler` classe é usada para processar solicitações de autenticação. É usado apenas para autenticação de nome de usuário/senha.

Ao gerar o token de autenticação, a data de expiração do token deve ser especificada. Propriedades personalizadas também podem ser incluídas no token. Se definidas, essas propriedades ficarão visíveis para o servidor quando o token de autenticação for enviado em solicitações subsequentes. Consulte [Manuseio de solicitações](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-handling-license-reqs.md) de licença para obter informações sobre como manipular tokens de autenticação personalizados.

O manipulador lê uma solicitação de autenticação e analisa a mensagem de solicitação quando `parseRequest()` é chamada. A implementação do servidor examina as credenciais do usuário na solicitação e, se as credenciais forem válidas, gera um `AuthenticationToken` objeto chamando `getRequest().generateAuthToken()`. Se não `AuthenticationRequestMessage.generateAuthToken()` for chamado antes `close()`, um código de erro de falha de autenticação será enviado.

* A classe do manipulador de solicitação é `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Se o protocolo de suporte do cliente e do servidor versão 5, o URL da solicitação será &quot;URL do servidor de licença nos metadados: + &quot;/flashaccess/authn/v4&quot;. Se a versão 3 do protocolo for o máximo suportado pelo cliente ou servidor, os clientes do Adobe Access enviarão solicitações de autenticação para &quot;URL do License Server em metadados&quot; + &quot;/flashaccess/authn/v3&quot;. Caso contrário, as solicitações de autenticação serão enviadas para &quot;URL do License Server em metadados&quot; + &quot;/flashaccess/authn/v1&quot;

