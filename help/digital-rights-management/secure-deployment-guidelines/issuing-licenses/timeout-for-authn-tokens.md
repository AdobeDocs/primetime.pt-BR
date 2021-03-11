---
description: Todos os tokens de autenticação gerados pelo SDK do DRM da Adobe Primetime têm um intervalo de tempo limite para proteger a segurança do aplicativo.
title: Tempo limite para tokens de autenticação
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Tempo limite para tokens de autenticação{#timeout-for-authentication-tokens}

Todos os tokens de autenticação gerados pelo SDK do DRM da Adobe Primetime têm um intervalo de tempo limite para proteger a segurança do aplicativo.

A expiração do token de autenticação é especificada e use o SDK de DRM do Primetime ao manipular uma solicitação de autenticação. Depois de expirar, o token não é mais válido e o usuário deve autenticar novamente com o servidor de licenças.

Para saber mais sobre solicitações de autenticação, consulte [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).
