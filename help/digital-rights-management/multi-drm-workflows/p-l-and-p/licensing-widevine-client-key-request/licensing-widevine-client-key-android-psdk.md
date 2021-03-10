---
description: O código do cliente transmite dados para uma API do Android.
title: Fluxo de trabalho de solicitação principal no Android PSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Fluxo de trabalho de solicitação principal no Android PSDK{#key-request-workflow-on-android-psdk}

O código do cliente transmite dados para uma API do Android.

No Android, seu código de cliente deve transmitir o URL do servidor de licença e os dados de aquisição de licença que o acompanham usando a seguinte API:

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

Depois de chamar essa API com sucesso, seu código pode iniciar a reprodução do conteúdo da maneira usual. Se você estiver usando o Express, é possível passar o token como parte do URL do servidor de licenças ou como uma propriedade de solicitação e retirar o token do URL do servidor de licenças.

Alguns dispositivos Android suportam Widevine e PlayReady. Nesses dispositivos, o cliente pode forçar o PSDK a descriptografar o conteúdo usando um DRM específico se o conteúdo tiver vários cabeçalhos de DRM. Isso pode ser feito chamando a seguinte API antes da reprodução:

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

