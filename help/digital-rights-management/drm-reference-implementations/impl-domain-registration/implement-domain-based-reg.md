---
title: Implementar o registro de domínio com base em identidade
description: Implementar o registro de domínio com base em identidade
copied-description: true
exl-id: e2f826a8-eea5-4d5f-ac4d-401d7a6c5373
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
