---
seo-title: Autenticação do usuário
title: Autenticação do usuário
uuid: 5cbd76b9-ff64-4a4b-8cfd-54f05c04eaa3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Autenticação de usuário {#user-authentication}

Uma solicitação do Adobe Primetime DRM pode conter um token de autenticação.

Se a autenticação de nome de usuário/senha tiver sido usada, a solicitação poderá incluir um `AuthenticationToken` gerado pelo `AuthenticationHandler`. Se quiser acessar e verificar o token, é necessário usar `RequestMessageBase.getAuthenticationToken()`. Para iniciar uma solicitação de nome de usuário/senha no cliente, use o ActionScript `DRMManager.authenticate()` ou a API do iOS.

Se o cliente e o servidor usarem um mecanismo de autenticação personalizado, o cliente obterá um token de autenticação por meio de outro canal e definirá o token de autenticação personalizado usando a API `DRMManager.setAuthenticationToken` do ActionScript 3.0. Use `RequestMessageBase.getRawAuthenticationToken()` para obter o token de autenticação personalizado. A implementação do servidor determina se o token de autenticação personalizado é válido.
