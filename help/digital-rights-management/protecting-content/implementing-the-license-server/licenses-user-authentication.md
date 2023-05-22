---
title: Autenticação do usuário
description: Autenticação do usuário
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Autenticação do usuário {#user-authentication}

Uma solicitação DRM do Adobe Primetime pode conter um token de autenticação.

Se a autenticação de nome de usuário/senha foi usada, a solicitação pode incluir um `AuthenticationToken` gerado pelo `AuthenticationHandler`. Se quiser acessar e verificar o token, é necessário usar `RequestMessageBase.getAuthenticationToken()`. Para iniciar uma solicitação de nome de usuário/senha no cliente, use o `DRMManager.authenticate()` API do ActionScript ou iOS.

Se o cliente e o servidor usarem um mecanismo de autenticação personalizado, o cliente obterá um token de autenticação por meio de algum outro canal e definirá o token de autenticação personalizado usando o `DRMManager.setAuthenticationToken` API do ActionScript 3.0. Uso `RequestMessageBase.getRawAuthenticationToken()` para obter o token de autenticação personalizado. A implementação do servidor determina se o token de autenticação personalizado é válido.
