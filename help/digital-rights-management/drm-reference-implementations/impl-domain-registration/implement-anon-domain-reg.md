---
seo-title: Implementar o registro de domínio anônimo
title: Implementar o registro de domínio anônimo
uuid: 330d32fd-8c23-40f9-949b-635e5a9acc86
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# Implementar o registro de domínio anônimo{#implement-anonymous-domain-registration}

1. Crie uma política de DRM que especifique que o registro de domínio é obrigatório.
1. Especifique o URL do servidor de domínio como:

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. Tornar a autenticação anônima obrigatória.

   No arquivo [!DNL .properties], defina:

   ```
   policy.domain.anonymous=true 
   ```
