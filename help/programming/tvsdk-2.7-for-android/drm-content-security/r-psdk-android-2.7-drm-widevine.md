---
description: Você pode usar o DRM nativo da Widevine do Android com fluxos DASH.
title: DRM de widevina
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# DRM {#widevine-drm} da janela

Você pode usar o DRM nativo da Widevine do Android com fluxos DASH.

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
* `requestProperties` - Contém cabeçalhos extras para incluir na solicitação de licença de saída.

Por exemplo, ao usar o conteúdo empacotado para o DRM de exibição, use o seguinte código antes de reproduzir:

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```

