---
title: Implementar o registro de domínio anônimo
description: Implementar o registro de domínio anônimo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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

1. Torne a autenticação anônima obrigatória.

   No arquivo [!DNL .properties], defina:

   ```
   policy.domain.anonymous=true 
   ```
