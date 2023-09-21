---
title: Implementar o registro de domínio com base em identidade
description: Implementar o registro de domínio com base em identidade
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# Implementar o registro de domínio com base em identidade{#implement-identity-based-domain-registration}

1. Crie uma política DRM com registro de domínio obrigatório.
1. Especifique o host e a porta do servidor para o URL do servidor de domínio.

   No seu [!DNL .properties] arquivo, definir:

   ```
   policy.domain.url=https://[server:port] 
   ```

1. Tornar a autenticação com um nome de usuário e senha obrigatória.

   No seu [!DNL .properties] arquivo, definir:

   ```
   policy.domain.anonymous=false 
   ```
