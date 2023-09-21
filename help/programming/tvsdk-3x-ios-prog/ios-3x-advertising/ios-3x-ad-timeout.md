---
description: É possível inserir anúncios em VOD e conteúdo dinâmico/linear usando a interface de decisão de anúncios do Adobe Primetime.
title: Exigências para publicidade
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Tempo limite do anúncio {#ad-timeout}

## Requisitos de base do AV {#av-foundation-requirements}

No caso de conteúdo VOD, a compilação da lista de reprodução, que envolve o carregamento do manifesto do conteúdo principal, a resolução do anúncio e o carregamento do manifesto do anúncio, deve ser concluída em 35 segundos.

No caso de conteúdo Live, cada vez que a lista de reprodução é atualizada, a compilação dela deve ser concluída em 20 segundos

**APIs relevantes para o Tempo limite de AdResolution**

```
/** @name Properties */
/** The default timeout value (in seconds) for resolution of ad requests is 15 seconds.
*
*/
*
@property (notatomic, assign) double adResolutionTimeout;
```

É possível definir adResolutionTimeout definindo PTAdMetadata::adResolutionTimeout ao configurar os metadados de anúncios.

```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adResolutionTimeout = 15 seconds
```

Em seguida, siga a seção: [Metadados do servidor de publicidade do Primetime](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

**APIs relevantes ao tempo limite do AdManifest**

```
/** @name Properties */
 /** The default timeout value (in seconds) for loading of ad manifests is 5 seconds.
 *
 */
 *
 @property (notatomic, assign) double adManifestTimeout; 
```

É possível definir adManifestTimeout definindo PTAdMetadata::adManifestTimeout ao configurar os metadados de anúncios.


```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adManifestTimeout = 5 seconds
```

Em seguida, siga a seção: [Metadados do servidor de publicidade do Primetime](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
