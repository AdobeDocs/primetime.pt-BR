---
title: Implementar registro de domínio anônimo
description: Implementar registro de domínio anônimo
copied-description: true
exl-id: 304cfe6f-0917-42ef-a49a-e6c4bc9c10d0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
