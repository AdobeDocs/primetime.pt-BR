---
description: O código do cliente transmite dados para uma API do Android.
seo-description: O código do cliente transmite dados para uma API do Android.
seo-title: Fluxo de trabalho de solicitação de chave no Android PSDK
title: Fluxo de trabalho de solicitação de chave no Android PSDK
uuid: 575163de-0f96-434d-a3ff-7e114caf72de
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Fluxo de trabalho de solicitação de chave no Android PSDK{#key-request-workflow-on-android-psdk}

O código do cliente transmite dados para uma API do Android.

No Android, seu código de cliente deve passar o URL do servidor de licença e os dados de aquisição de licença associados usando a seguinte API:

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

Depois de chamar essa API com êxito, seu código pode iniciar a reprodução do conteúdo da maneira habitual. Se você estiver usando o Express, poderá passar o token como parte do URL do servidor de licenças ou como uma propriedade de solicitação e retirar o token do URL do servidor de licenças.

Alguns dispositivos Android suportam Widevine e PlayReady. Nesses dispositivos, o cliente pode querer forçar o PSDK a descriptografar o conteúdo usando um DRM específico se o conteúdo tiver vários cabeçalhos DRM. Isso pode ser feito chamando a seguinte API antes da reprodução:

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

