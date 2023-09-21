---
title: Tempo limite para tokens de autenticação
description: Tempo limite para tokens de autenticação
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Tempo limite para tokens de autenticação{#timeout-for-authentication-tokens}

Todos os tokens de autenticação gerados pelo SDK do Adobe Access têm um intervalo de tempo limite para proteger a segurança do aplicativo. A expiração do token de autenticação é especificada ao usar o SDK de acesso do Adobe ao manipular uma solicitação de autenticação. Após a expiração, o token de autenticação não será mais válido e o usuário deverá autenticar novamente no servidor de licenças.

Para saber mais sobre solicitações de autenticação, consulte AuthenticationHandler no *Referência da API de acesso do Adobe*.
