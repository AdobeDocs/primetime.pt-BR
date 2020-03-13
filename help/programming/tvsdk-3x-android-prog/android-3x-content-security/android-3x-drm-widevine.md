---
description: Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao seu conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa à solução integrada da Adobe.
seo-description: Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao seu conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa à solução integrada da Adobe.
seo-title: DRM widevine
title: DRM widevine
uuid: 3a5fd786-4319-4e92-83b6-0f5328df6a44
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# DRM widevine {#widevine-drm}

Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao seu conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa à solução integrada da Adobe.

Entre em contato com seu representante da Adobe para obter as informações mais atualizadas sobre a disponibilidade de soluções de DRM de terceiros.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

Você pode usar o DRM nativo do Android Widevine com fluxos DASH.

Chame a seguinte API antes de iniciar a reprodução: `com.adobe.mediacore.drm.DRMManager`

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

Argumentos:

* `drm` - `"com.widevine.alpha"` Widevine.

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
