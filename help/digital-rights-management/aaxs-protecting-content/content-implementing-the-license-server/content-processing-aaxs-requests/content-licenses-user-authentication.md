---
title: Autenticação do usuário
description: Autenticação do usuário
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Autenticação do usuário{#user-authentication}

Uma solicitação de Acesso a Adobe pode conter um token de autenticação.

Se a autenticação de nome de usuário/senha foi usada, a solicitação pode conter um `AuthenticationToken` gerado pelo `AuthenticationHandler`. Para acessar e verificar o token, use `RequestMessageBase.getAuthenticationToken()`. Para iniciar uma solicitação de nome de usuário/senha no cliente, use o ActionScript `DRMManager.authenticate()` ou a API do iOS.

Se o cliente e o servidor estiverem usando um mecanismo de autenticação personalizado, o cliente obterá um token de autenticação por meio de outro canal e definirá o token de autenticação personalizado usando a API `DRMManager.setAuthenticationToken` ActionScript 3.0. Use `RequestMessageBase.getRawAuthenticationToken()` para obter o token de autenticação personalizado. A implementação do servidor é responsável por determinar se o token de autenticação personalizado é válido.
