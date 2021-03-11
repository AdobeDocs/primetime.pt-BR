---
title: Carregamento de anúncio seguro por HTTPS
description: Carregamento de anúncio seguro por HTTPS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Carregamento de anúncio seguro por HTTPS{#secure-ad-loading-over-https}

A Adobe Primetime pode solicitar servidores de publicidade de terceiros em https, mesmo se o reprodutor estiver hospedado em http. Somente essas chamadas de servidores de anúncios são atualizadas para https que o cliente procura durante a fase do resolvedor de anúncios do Auditude.

>[!NOTE]
>
>Este recurso não é compatível com o Flash.

Use o seguinte para ativar o carregamento seguro de anúncios. Não está habilitado por padrão.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
