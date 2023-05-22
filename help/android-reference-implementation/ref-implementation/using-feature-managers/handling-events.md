---
description: Se o aplicativo precisar manipular eventos despachados do gerenciador de recursos, ele precisará registrar o gerenciador no arquivo PlayerFragment.java.
title: Manipulação de eventos
exl-id: 4c9a76bb-071e-4408-819c-a7611fe615cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Manipulação de eventos {#handling-events}

Se o aplicativo precisar manipular eventos despachados do gerenciador de recursos, ele precisará registrar o gerenciador no arquivo PlayerFragment.java.

Por exemplo:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
