---
seo-title: Autenticação do usuário
title: Autenticação do usuário
uuid: 191964eb-cd68-47a6-8214-aec01f993df4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Autenticação do usuário{#user-authentication}

Uma solicitação de acesso a Adobe pode conter um token de autenticação.

Se a autenticação de nome de usuário/senha tiver sido usada, a solicitação poderá conter um `AuthenticationToken` gerado pelo `AuthenticationHandler`. Para acessar e verificar o token, use `RequestMessageBase.getAuthenticationToken()`. Para iniciar uma solicitação de nome de usuário/senha no cliente, use o ActionScript `DRMManager.authenticate()` ou a API do iOS.

Se o cliente e o servidor estiverem usando um mecanismo de autenticação personalizado, o cliente obterá um token de autenticação por meio de outro canal e definirá o token de autenticação personalizado usando a API `DRMManager.setAuthenticationToken` do ActionScript 3.0. Use `RequestMessageBase.getRawAuthenticationToken()` para obter o token de autenticação personalizado. A implementação do servidor é responsável por determinar se o token de autenticação personalizado é válido.
