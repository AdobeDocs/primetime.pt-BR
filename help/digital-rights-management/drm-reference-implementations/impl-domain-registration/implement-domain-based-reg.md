---
seo-title: Implementar o registro de domínio baseado em identidade
title: Implementar o registro de domínio baseado em identidade
uuid: 4a71b2e0-d1a2-4d63-9cbd-980a292774ab
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
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

1. Torne a autenticação obrigatória com um nome de usuário e senha.

   No arquivo [!DNL .properties], defina:

   ```
   policy.domain.anonymous=false 
   ```
