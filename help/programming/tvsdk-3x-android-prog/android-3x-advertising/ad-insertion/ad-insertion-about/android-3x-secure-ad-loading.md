---
title: Carregamento de anúncio seguro em HTTPS
description: Carregamento de anúncio seguro em HTTPS
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Carregamento de anúncio seguro em HTTPS {#secure-ad-loading-over-https}

O Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios Primetime e as chamadas relacionadas ao CRS por HTTPS.

O recurso não está habilitado por padrão. Use o seguinte para ativar o carregamento seguro de anúncios.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
