---
title: Implementar o registro de domínio baseado na identidade
description: Implementar o registro de domínio baseado na identidade
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Implementar o registro de domínio baseado em identidade{#implement-identity-based-domain-registration}

1. Crie uma política de DRM com registro de domínio obrigatório.
1. Especifique o host e a porta do servidor para o URL do servidor de domínio.

   No arquivo [!DNL .properties], defina:

   ```
   policy.domain.url=https://[server:port] 
   ```

1. Torne a autenticação obrigatória com nome de usuário e senha.

   No arquivo [!DNL .properties], defina:

   ```
   policy.domain.anonymous=false 
   ```
