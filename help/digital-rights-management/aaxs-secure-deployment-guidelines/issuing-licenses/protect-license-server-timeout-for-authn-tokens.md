---
title: Tempo limite para tokens de autenticação
description: Tempo limite para tokens de autenticação
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Tempo limite para tokens de autenticação{#timeout-for-authentication-tokens}

Todos os tokens de autenticação gerados pelo SDK do Adobe Access têm um intervalo de tempo limite para proteger a segurança do aplicativo. A expiração do token de autenticação é especificada e use o SDK de Acesso ao Adobe ao manipular uma solicitação de autenticação. Depois que a expiração for aprovada, o token de autenticação não será mais válido e o usuário deverá autenticar novamente com o servidor de licenças.

Para saber mais sobre solicitações de autenticação, consulte AuthenticationHandler na *Referência da API de Acesso ao Adobe*.
