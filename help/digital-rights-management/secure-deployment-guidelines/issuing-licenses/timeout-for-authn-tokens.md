---
description: Todos os tokens de autenticação gerados pelo SDK do Adobe Primetime DRM têm um intervalo de tempo limite para proteger a segurança do aplicativo.
seo-description: Todos os tokens de autenticação gerados pelo SDK do Adobe Primetime DRM têm um intervalo de tempo limite para proteger a segurança do aplicativo.
seo-title: Tempo limite para tokens de autenticação
title: Tempo limite para tokens de autenticação
uuid: 2c2b0dad-0979-4d49-b109-2700ceb4d722
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Tempo limite para tokens de autenticação{#timeout-for-authentication-tokens}

Todos os tokens de autenticação gerados pelo SDK do Adobe Primetime DRM têm um intervalo de tempo limite para proteger a segurança do aplicativo.

A expiração do token de autenticação é especificada. Use o SDK do Primetime DRM ao manipular uma solicitação de autenticação. Depois de expirar, o token não é mais válido e o usuário deve autenticar novamente com o servidor de licenças.

Para saber mais sobre solicitações de autenticação, consulte [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).
