---
description: Todos os tokens de autenticação gerados pelo SDK do Adobe Primetime DRM têm um intervalo de tempo limite para proteger a segurança do aplicativo.
title: Tempo limite para tokens de autenticação
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Tempo limite para tokens de autenticação{#timeout-for-authentication-tokens}

Todos os tokens de autenticação gerados pelo SDK do Adobe Primetime DRM têm um intervalo de tempo limite para proteger a segurança do aplicativo.

A expiração do token de autenticação é especificada ao usar o SDK DRM do Primetime ao manipular uma solicitação de autenticação. Após a expiração, o token não é mais válido e o usuário deve se autenticar novamente no servidor de licenças.

Para saber mais sobre solicitações de autenticação, consulte [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).
