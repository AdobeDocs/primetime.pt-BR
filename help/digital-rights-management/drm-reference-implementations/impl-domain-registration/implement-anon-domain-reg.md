---
title: Implementar registro de domínio anônimo
description: Implementar registro de domínio anônimo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# Implementar registro de domínio anônimo{#implement-anonymous-domain-registration}

1. Crie uma política DRM que especifique que o registro de domínio é necessário.
1. Especifique o URL do servidor de domínio como:

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. Tornar a autenticação anônima obrigatória.

   No seu [!DNL .properties] arquivo, definir:

   ```
   policy.domain.anonymous=true 
   ```
