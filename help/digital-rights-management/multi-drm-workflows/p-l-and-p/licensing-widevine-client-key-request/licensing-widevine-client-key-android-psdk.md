---
description: O código do cliente passa dados para uma API Android.
title: Fluxo de trabalho de solicitação principal no Android PSDK
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Fluxo de trabalho de solicitação principal no Android PSDK{#key-request-workflow-on-android-psdk}

O código do cliente passa dados para uma API Android.

No Android, o código de cliente deve passar o URL do servidor de licenças e os dados de aquisição de licença que o acompanham usando a seguinte API:

```
class DRMManager 
   { 
   ... 
   /* 
   * Set the license server URL and attached request properties that the PSDK should use for the passed in drm type.  
   * 
   * drmType: "com.widevine.alpha" for widevine. "com.microsoft.playready" for playready. 
   * licenseServerURL: self explanatory.  
   * requestProperties: key value pairs to be attached as HTTP headers to all license request sent to the passed in license server URL. Pass in 
   * NULL if none is needed.  
   */ 
   public static void setProtectionData(String drmType, String licenseServerURL,  Map<String, String> requestProperties); 
    }
```

Depois de chamar essa API com êxito, seu código pode iniciar a reprodução de conteúdo da maneira usual. Se você estiver usando o ExpressPlay, é possível passar o token como parte do URL do servidor de licença ou como uma propriedade de solicitação e retirar o token do URL do servidor de licença.

Alguns dispositivos Android são compatíveis com Widevine e PlayReady. Nesses dispositivos, o cliente pode forçar o PSDK a descriptografar o conteúdo usando um DRM específico, se o conteúdo tiver vários cabeçalhos DRM. Isso pode ser feito chamando a seguinte API antes da reprodução:

```
class MediaPlayer 
   { 
   ... 
    
   /* 
   * drm: pass in "com.widevine.alpha" for widevine or "com.microsoft.playready" for playready 
   * 
   */ 
   public void setDRMScheme(String drm) throws MediaPlayerException 
   }
```
