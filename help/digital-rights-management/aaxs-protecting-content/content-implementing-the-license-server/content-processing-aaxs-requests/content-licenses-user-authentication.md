---
title: Autenticação do usuário
description: Autenticação do usuário
copied-description: true
exl-id: a0dd7d81-2249-4845-94da-53b755d6cd7c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Autenticação do usuário{#user-authentication}

Uma solicitação de Acesso ao Adobe pode conter um token de autenticação.

Se uma autenticação de nome de usuário/senha foi usada, a solicitação pode conter uma `AuthenticationToken` gerado pelo `AuthenticationHandler`. Para acessar e verificar o token, use `RequestMessageBase.getAuthenticationToken()`. Para iniciar uma solicitação de nome de usuário/senha no cliente, use o `DRMManager.authenticate()` API do ActionScript ou iOS.

Se o cliente e o servidor estiverem usando um mecanismo de autenticação personalizado, o cliente obterá um token de autenticação por meio de algum outro canal e definirá o token de autenticação personalizado usando o `DRMManager.setAuthenticationToken` API do ActionScript 3.0. Uso `RequestMessageBase.getRawAuthenticationToken()` para obter o token de autenticação personalizado. A implementação do servidor é responsável por determinar se o token de autenticação personalizado é válido.
