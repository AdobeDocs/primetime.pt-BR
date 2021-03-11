---
description: Você pode inserir anúncios no VOD e conteúdo ao vivo/linear usando a interface do Adobe Primetime Ad Decisioning.
title: Requisitos de publicidade
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Tempo limite do anúncio {#ad-timeout}

## Requisitos básicos do AV {#av-foundation-requirements}

No caso de conteúdo VOD, a compilação da lista de reprodução, que envolve o carregamento do manifesto do conteúdo principal, a resolução do anúncio e o carregamento do manifesto do anúncio, deve ser concluída em 35 segundos.

No caso de conteúdo em tempo real, cada vez que a lista de reprodução é atualizada, a compilação da lista de reprodução deve ser concluída em 20 segundos

**APIs relevantes ao Tempo limite da AdResolution**

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

Logo após, siga a seção : [Metadados do servidor de anúncio do Primetime](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

**APIs relevantes ao Tempo limite AdManifest**

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

Logo após, siga a seção : [Metadados do servidor de anúncio do Primetime](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
