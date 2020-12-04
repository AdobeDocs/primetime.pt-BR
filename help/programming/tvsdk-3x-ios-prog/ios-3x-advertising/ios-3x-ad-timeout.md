---
description: Você pode inserir publicidades em seu VOD e conteúdo ao vivo/linear usando a interface de decisão de publicidade da Adobe Primetime.
seo-description: Você pode inserir publicidades em seu VOD e conteúdo ao vivo/linear usando a interface de decisão de publicidade da Adobe Primetime.
seo-title: Requisitos de publicidade
title: Requisitos de publicidade
uuid: 0287f1e4-746f-42e5-b811-409064dd9b13
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Tempo limite do anúncio {#ad-timeout}

## Requisitos do AV Foundation {#av-foundation-requirements}

No caso de conteúdo VOD, a identificação da lista de reprodução, que envolve o carregamento do manifesto do conteúdo principal, a resolução do anúncio e o carregamento do manifesto do anúncio, deve ser concluída dentro de 35 segundos.

No caso de conteúdo ao vivo, cada vez que a lista de reprodução é atualizada, a identificação da lista de reprodução deve ser concluída em 20 segundos

**APIs relevantes ao Tempo limite de AdResolution**

```
/** @name Properties */
/** The default timeout value (in seconds) for resolution of ad requests is 15 seconds.
*
*/
*
@property (notatomic, assign) double adResolutionTimeout;
```

Você pode definir adResolutionTimeout definindo PTAdMetadata::adResolutionTimeout ao configurar os metadados do anúncio.

```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adResolutionTimeout = 15 seconds
```

A seguir à seção: [Metadados do servidor de anúncio Primetime](../..//tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

**APIs relevantes ao tempo limite do AdManifest**

```
/** @name Properties */
 /** The default timeout value (in seconds) for loading of ad manifests is 5 seconds.
 *
 */
 *
 @property (notatomic, assign) double adManifestTimeout; 
```

Você pode definir adManifestTimeout definindo PTAdMetadata::adManifestTimeout ao configurar os metadados do anúncio.


```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adManifestTimeout = 5 seconds
```

A seguir à seção: [Metadados do servidor de anúncio Primetime](../..//tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
