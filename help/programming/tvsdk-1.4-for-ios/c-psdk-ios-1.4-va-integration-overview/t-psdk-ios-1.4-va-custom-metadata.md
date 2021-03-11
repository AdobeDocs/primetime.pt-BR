---
description: Você pode fornecer metadados personalizados sobre conteúdo, anúncios e chamadas de rastreamento de capítulo usando funções de retorno de chamada.
title: Implementar o suporte a metadados personalizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---


# Implementar o suporte a metadados personalizados{#implement-custom-metadata-support}

Você pode fornecer metadados personalizados sobre conteúdo, anúncios e chamadas de rastreamento de capítulo usando funções de retorno de chamada.

As funções de retorno de chamada são chamadas logo antes da chamada de rastreamento ser feita, de modo que seu aplicativo possa anexar os metadados específicos a um anúncio ou capítulo.

Chame funções de retorno de chamada para conteúdo, anúncios e capítulos.

```
// Video Metadata Block 
    vaTrackingMetadata.videoMetadataBlock = ^NSDictionary *() 
    { 
        return @{ 
                 @"myvideoid": @"1234", 
                 @"mysdkversion": [PTSDK apiVersion] 
                 }; 
    }; 
      
// Ad Metadata Block invoked on every ad start 
    vaTrackingMetadata.adMetadataBlock = ^NSDictionary *(PTAd *ad) 
    { 
        return @{ 
                 @"myadid": @"ad-1234", 
                 @"myad-sdkversion": [PTSDK apiVersion] 
                 }; 
    }; 
      
// Chapter Metadata Block invoked on every chapter start 
    vaTrackingMetadata.chapterMetadataBlock = ^NSDictionary *(PTVideoAnalyticsChapterData *chapter) 
    { 
        return @{ 
                 @"mychapterid": @"chapter-1234", 
                 @"mychapter-sdkversion": [PTSDK apiVersion] 
                 }; 
    };
```

