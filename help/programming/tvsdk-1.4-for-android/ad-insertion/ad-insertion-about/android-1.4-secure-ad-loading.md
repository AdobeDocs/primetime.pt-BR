---
description: nulo
seo-description: nulo
seo-title: Carregamento de anúncio seguro por HTTPS
title: Carregamento de anúncio seguro por HTTPS
uuid: 0d680fef-a372-4157-a89b-d9f10003c768
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Carregamento de anúncio seguro por HTTPS{#secure-ad-loading-over-https}

O Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios Primetime e para chamadas relacionadas a CRS por HTTPS.

O recurso não está ativado por padrão. Use o seguinte para ativar o carregamento seguro de anúncios.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

