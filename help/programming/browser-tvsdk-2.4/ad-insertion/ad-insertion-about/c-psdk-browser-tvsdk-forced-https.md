---
title: Carregamento de anúncio seguro em HTTPS
description: Carregamento de anúncio seguro em HTTPS
copied-description: true
exl-id: d43418e9-631b-4344-a5b3-0a6154a325d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# Carregamento de anúncio seguro em HTTPS{#secure-ad-loading-over-https}

O Adobe Primetime pode solicitar servidores de publicidade de terceiros por https, mesmo se o reprodutor estiver hospedado em http. Somente essas chamadas de servidores de anúncios são atualizadas para https que o cliente busca durante a fase do resolvedor de anúncios do Auditude.

>[!NOTE]
>
>Este recurso não é compatível com o Flash.

Use o seguinte para ativar o carregamento seguro de anúncios. Ela não está ativada por padrão.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
