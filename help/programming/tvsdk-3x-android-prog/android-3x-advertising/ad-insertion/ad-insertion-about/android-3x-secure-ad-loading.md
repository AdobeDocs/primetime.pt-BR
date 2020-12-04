---
description: nulo
seo-description: nulo
seo-title: Carregamento de anúncio seguro por HTTPS
title: Carregamento de anúncio seguro por HTTPS
uuid: 18be77cc-c59b-4982-b8c1-e4451495edd2
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# Carregamento de anúncio seguro em HTTPS {#secure-ad-loading-over-https}

A Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios Primetime e as chamadas relacionadas a CRS por HTTPS.

O recurso não está ativado por padrão. Use o seguinte para ativar o carregamento seguro de anúncios.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
