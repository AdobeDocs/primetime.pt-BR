---
description: Você pode usar o DRM Widevine nativo do Android com fluxos DASH.
title: DRM Widevine
exl-id: 6a011cd7-446a-4f3a-ae36-110618001bf3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
