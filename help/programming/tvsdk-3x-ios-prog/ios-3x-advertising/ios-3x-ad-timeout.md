---
description: Você pode inserir publicidades em seu VOD e conteúdo ao vivo/linear usando a interface de decisão do anúncio do Adobe Primetime.
seo-description: Você pode inserir publicidades em seu VOD e conteúdo ao vivo/linear usando a interface de decisão do anúncio do Adobe Primetime.
seo-title: Requisitos de publicidade
title: Requisitos de publicidade
uuid: 0287f1e4-746f-42e5-b811-409064dd9b13
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Tempo limite do anúncio {#ad-timeout}

## Requisitos do AV Foundation {#av-foundation-requirements}

No caso de conteúdo VOD, a identificação da lista de reprodução, que envolve o carregamento do manifesto do conteúdo principal, a resolução do anúncio e o carregamento do manifesto do anúncio, deve ser concluída dentro de 35 segundos.

No caso de conteúdo ao vivo, cada vez que a lista de reprodução é atualizada, a identificação da lista de reprodução deve ser concluída em 20 segundos

**APIs relevantes ao tempo limite de AdResolution**

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

A seguir à seção: Metadados [](../..//tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md)do servidor de anúncios do Primetime.

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

A seguir à seção: Metadados [](../..//tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md)do servidor de anúncios do Primetime.
