---
title: Carregamento de anúncio seguro em HTTPS
description: Carregamento de anúncio seguro em HTTPS
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# Carregamento de anúncio seguro em HTTPS{#secure-ad-loading-over-https}

O Adobe Primetime pode solicitar servidores de publicidade de terceiros por https, mesmo se o reprodutor estiver hospedado em http. Somente essas chamadas de servidores de anúncios são atualizadas para https que o cliente busca durante a fase do resolvedor de anúncios Auditude.

>[!NOTE]
>
>Este recurso não é compatível com o Flash.

Use o seguinte para ativar o carregamento seguro de anúncios. Ela não está ativada por padrão.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
