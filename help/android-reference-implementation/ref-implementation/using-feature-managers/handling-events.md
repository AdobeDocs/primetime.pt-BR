---
description: Se o aplicativo precisar manipular eventos despachados do gerenciador de recursos, ele precisará registrar o gerenciador no arquivo PlayerFragment.java.
title: Manipulação de eventos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
