---
description: Você pode usar o DRM nativo do Android Widevine com fluxos DASH.
seo-description: Você pode usar o DRM nativo do Android Widevine com fluxos DASH.
seo-title: DRM widevine
title: DRM widevine
uuid: ceb2f18f-9e53-47d6-9d4b-7004ac1d22c9
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---


# DRM de largura {#widevine-drm}

Você pode usar o DRM nativo do Android Widevine com fluxos DASH.

Chame a seguinte API `com.adobe.mediacore.drm.DRMManager` antes de iniciar a reprodução:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

Argumentos:

* `drm` -  `"com.widevine.alpha"` para Widevine.

* `licenseServerURL` - O URL do servidor de licenças do Widevine que recebe solicitações de licença.
* `requestProperties` - Contém cabeçalhos adicionais para incluir na solicitação de licença de saída.

Por exemplo, ao usar o conteúdo empacotado para o DRM de apresentação, use o seguinte código antes de reproduzir:

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```

