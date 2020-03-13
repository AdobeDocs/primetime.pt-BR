---
description: nulo
seo-description: nulo
seo-title: Carregamento de anúncio seguro por HTTPS
title: Carregamento de anúncio seguro por HTTPS
uuid: 72ab94d3-ee0c-4f02-adf2-c186ae6aec26
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Carregamento de anúncio seguro por HTTPS {#secure-ad-loading-over-https}

O Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios Primetime e para chamadas relacionadas a CRS por HTTPS.

O recurso não está ativado por padrão. Use o seguinte para ativar o carregamento seguro de anúncios.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

