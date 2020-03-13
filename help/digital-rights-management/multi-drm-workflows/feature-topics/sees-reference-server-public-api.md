---
description: A solicitação de direito e a resposta são passadas por uma conexão SSL mutuamente autenticada entre o servidor de licença e o serviço de direito do cliente.
seo-description: A solicitação de direito e a resposta são passadas por uma conexão SSL mutuamente autenticada entre o servidor de licença e o serviço de direito do cliente.
seo-title: API pública do SEES
title: API pública do SEES
uuid: f3a17d61-04ee-4bdb-9d64-a98066c6d1c8
translation-type: tm+mt
source-git-commit: 15403abbd53486e1faa2146cda83f41bd8116632

---


# API pública do SEES {#sees-public-api}

A solicitação de direito e a resposta são passadas por uma conexão SSL mutuamente autenticada entre o servidor de licença e o serviço de direito do cliente.

O esquema URI HTTPS ( [https://tools.ietf.org/html/rfc7230#section-2.7.2](https://tools.ietf.org/html/rfc7230#section-2.7.2)) é usado para definir o ponto final de direito e o método de solicitação HTTP POST ( [https://tools.ietf.org/html/rfc7231#section-4.3.3](https://tools.ietf.org/html/rfc7231#section-4.3.3)) é usado para a solicitação. O endpoint de direito, bem como um sinalizador que indica o direito de back-end, é obrigatório e deve ser incluído na política no momento do empacotamento.

## Solicitação de direito {#section_BFBFEF0795CA46D6842C479256B95F95}

O corpo da solicitação de direito será um objeto JSON definido como mostrado abaixo.

**Definição de objeto de solicitação de direito JSON**

```
{ 
 "title" : "Entitlement Request", 
 "type" : "object", 
 "properties" : { 
  "messageID" : { 
   "type" : "string", 
   "description" : "Unique ID for this message (GUID).  Used to confirm that the subsequent response is actually for this request." 
  }, 
  "version" : { 
   "type" : "integer", 
   "description" : "Version number of the protocol, currently 1." 
  }, 
  "requestType" : { 
   "type" : "integer", 
   "description" : "Request type. 1 - time based entitlement request, 2 - device registration entitlement request 3 - device bound entitlement request." 
  }, 
  "contentID" : { 
   "type" : "string", 
   "description" : "Content ID (GUID) that was given to the content during packaging time." 
  }, 
  "customerCookie" : { 
   "type" : "string", 
   "description" : "Customer cookie. Cookie is just arbitrary string up to 32 characters long." 
  } 
    }, 
 "required" : ["messageID", "version", "contentID"] 
}
```

## Resposta de direito {#section_F15A9FD6BAD946B3B4C5C14612F90154}

O corpo da resposta de direito é um objeto JSON.

**Definição de objeto de resposta de direito JSON**

```
{ 
  "title" : "Entitlement Response", 
  "type" : "object", 
  "properties" : { 
    "messageID" : { 
    "type" : "string", 
    "description" : "Unique ID from the Entitlement Request message.   
      Must match, or entitlement will be denied." 
  }, 
  "version" : { 
    "type" : "integer", 
    "description" : "Version number of the protocol; must be <= the version number  
      from the Entitlement Request message." 
  }, 
  "isAllowed" : { 
    "type" : "boolean", 
    "description" : "Grant the license or not." 
  }, 
  "epTokenURL" : { 
    "type" : "string", 
    "description" : "ExpressPlay Token URL" 
  }, 
  "error" : { 
    "type" : "integer", 
    "description" : "An error number produced by the entitlement server.  
      Will be passed to the client as the 'code' field of the server error response." 
  }, 
  "errorText" : { 
    "type" : "string", 
    "description" : "Additional error information produced by the entitlement server.  
      Will be passed to the client as the 'text' field of the server error response." 
  }, 
  "required" : ["messageID", "version", "isAllowed", "epTokenURL"] 
}
```
