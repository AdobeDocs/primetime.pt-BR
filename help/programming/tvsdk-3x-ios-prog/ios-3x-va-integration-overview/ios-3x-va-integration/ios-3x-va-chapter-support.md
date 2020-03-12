---
description: nulo
seo-description: nulo
seo-title: Implementar suporte a capítulo
title: Implementar suporte a capítulo
uuid: b0e5ef1c-6568-4901-9ac7-261df71a0110
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Implementar suporte a capítulo {#implement-chapter-support}

Você pode definir e rastrear capítulos para rastreamento de vídeo em um aplicativo baseado em TVSDK das seguintes maneiras:

* Os capítulos padrão, que são gerenciados internamente pelo TVSDK.

   Um capítulo é definido como o tempo entre cada intervalo de anúncios. Por exemplo, o tempo entre uma pausa de anúncio precedente e o primeiro intermediário é definido como o primeiro capítulo.
* Os capítulos personalizados, que são gerenciados pelo aplicativo e são baseados em dados CMS ou de outra forma que o aplicativo usa para definir capítulos.

   Defina e rastreie capítulos padrão ou personalizados.

   ```
   // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
   
       vaTrackingMetadata.enableChapterTracking = YES; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata:  
   // For example, 3 chapters of 60 second duration each: 
   
       NSMutableArray *chapters = [[[NSMutableArray alloc] init] autorelease]; 
   
       int chapterDuration = 60; 
       for (int i = 0; i < 3; i++) 
       { 
           PTVideoAnalyticsChapterData *chapterData =  
             [[[PTVideoAnalyticsChapterData alloc] init] autorelease]; 
           chapterData.name = [NSString stringWithFormat:@"chapter_%d", (i+1)]; 
           chapterData.range =  
             CMTimeRangeMake(CMTimeMakeWithSeconds(i * chapterDuration, 10000),  
             CMTimeMakeWithSeconds(chapterDuration, 10000)); 
   
           [chapters addObject:chapterData]; 
       } 
   
       vaTrackingMetadata.chapters = chapters; 
   
   // For default chapters, the application must not set custom chapters on the tracking metadata  
   // and simply enable chapters to be tracked by setting the boolean value as defined above.
   ```
