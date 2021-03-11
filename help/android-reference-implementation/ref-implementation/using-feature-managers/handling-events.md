---
description: Se o aplicativo precisar lidar com eventos despachados do gerenciador de recursos, ele precisará registrar o gerenciador no arquivo PlayerFragment.java .
title: Manipulação de eventos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 4%

---


# Manipular eventos {#handling-events}

Se o aplicativo precisar lidar com eventos despachados do gerenciador de recursos, ele precisará registrar o gerenciador no arquivo PlayerFragment.java .

Por exemplo:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
