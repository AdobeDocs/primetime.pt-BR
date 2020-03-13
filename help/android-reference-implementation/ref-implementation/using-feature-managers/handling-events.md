---
description: Se o aplicativo precisar lidar com eventos despachados do gerenciador de recursos, ele precisará registrar o gerenciador no arquivo PlayerFragment.java.
seo-description: Se o aplicativo precisar lidar com eventos despachados do gerenciador de recursos, ele precisará registrar o gerenciador no arquivo PlayerFragment.java.
seo-title: Tratamento de eventos
title: Tratamento de eventos
uuid: 13639f02-0dcc-4a0a-8524-515da5478006
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Tratamento de eventos {#handling-events}

Se o aplicativo precisar lidar com eventos despachados do gerenciador de recursos, ele precisará registrar o gerenciador no arquivo PlayerFragment.java.

Por exemplo:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
