---
description: Você pode usar o DRM Widevine nativo do Android com fluxos DASH.
title: DRM Widevine
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# DRM Widevine {#widevine-drm}

Você pode usar o DRM Widevine nativo do Android com fluxos DASH.

Chame o seguinte `com.adobe.mediacore.drm.DRMManager` API antes de iniciar a reprodução:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

Argumentos:

* `drm` - `"com.widevine.alpha"` para Widevine.

* `licenseServerURL` - O URL do servidor de licenças Widevine que recebe solicitações de licença.
* `requestProperties` - Contém cabeçalhos extras a serem incluídos na solicitação de licença de saída.

Por exemplo, ao usar o conteúdo empacotado para o ExpressPlay DRM, use o seguinte código antes de reproduzir:

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```
