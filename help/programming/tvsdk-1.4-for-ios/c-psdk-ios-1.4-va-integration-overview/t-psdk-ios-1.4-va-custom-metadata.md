---
description: Você pode fornecer metadados personalizados sobre conteúdo, anúncios e chamadas de rastreamento de capítulo usando funções de retorno de chamada.
title: Implementar suporte a metadados personalizados
exl-id: c7478578-7f49-4fd0-b381-c558888401aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# Implementar suporte a metadados personalizados{#implement-custom-metadata-support}

Você pode fornecer metadados personalizados sobre conteúdo, anúncios e chamadas de rastreamento de capítulo usando funções de retorno de chamada.

As funções de retorno de chamada são chamadas antes da chamada de rastreamento ser feita, para que o aplicativo possa anexar os metadados específicos a um anúncio ou capítulo.

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
