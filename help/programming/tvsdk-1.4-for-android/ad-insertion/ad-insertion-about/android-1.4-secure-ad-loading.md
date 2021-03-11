---
title: Carregamento de anúncio seguro por HTTPS
description: Carregamento de anúncio seguro por HTTPS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# Carregamento de anúncio seguro por HTTPS{#secure-ad-loading-over-https}

A Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios Primetime e as chamadas relacionadas ao CRS por HTTPS.

O recurso não está habilitado por padrão. Use o seguinte para ativar o carregamento seguro de anúncios.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

