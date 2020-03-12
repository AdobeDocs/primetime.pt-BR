---
seo-title: Tempo limite para tokens de autenticação
title: Tempo limite para tokens de autenticação
uuid: 41b0fbf5-a567-4118-bec1-c05e6e0b6d1f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Tempo limite para tokens de autenticação{#timeout-for-authentication-tokens}

Todos os tokens de autenticação gerados pelo SDK do Adobe Access têm um intervalo de tempo limite para proteger a segurança do aplicativo. A expiração do token de autenticação é especificada. Use o SDK do Adobe Access ao manipular uma solicitação de autenticação. Após a expiração, o token de autenticação não é mais válido e o usuário deve autenticar novamente com o servidor de licenças.

Para saber mais sobre solicitações de autenticação, consulte AuthenticationHandler na Referência *da API do* Adobe Access.
