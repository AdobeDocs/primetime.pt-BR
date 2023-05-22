---
title: Tempo limite para tokens de autenticação
description: Tempo limite para tokens de autenticação
copied-description: true
exl-id: ee9c5b2c-6a79-499c-bd60-718e33bc3a9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Tempo limite para tokens de autenticação{#timeout-for-authentication-tokens}

Todos os tokens de autenticação gerados pelo SDK do Adobe Access têm um intervalo de tempo limite para proteger a segurança do aplicativo. A expiração do token de autenticação é especificada ao usar o SDK de acesso do Adobe ao manipular uma solicitação de autenticação. Após a expiração, o token de autenticação não será mais válido e o usuário deverá autenticar novamente no servidor de licenças.

Para saber mais sobre solicitações de autenticação, consulte AuthenticationHandler no *Referência da API de acesso do Adobe*.
