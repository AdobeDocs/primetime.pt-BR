---
description: nulo
seo-description: nulo
seo-title: Implementar suporte a capítulo
title: Implementar suporte a capítulo
uuid: 85d14b83-7910-4f5d-9ef2-511de916abd6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Implementar suporte a capítulo {#implement-chapter-support}

Você pode definir e rastrear capítulos para rastreamento de vídeo em um aplicativo baseado em TVSDK das seguintes maneiras:

* Os capítulos padrão, que são gerenciados internamente pelo TVSDK.

   Um capítulo é definido como o tempo entre cada intervalo de anúncios. Por exemplo, o tempo entre uma pausa de anúncio precedente e o primeiro intermediário é definido como o primeiro capítulo.
* Os capítulos personalizados, que são gerenciados pelo aplicativo e são baseados em dados CMS ou de outra forma que o aplicativo usa para definir capítulos.

   Defina e rastreie capítulos padrão ou personalizados.

   ```
   // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
   
       vaMetadata.enableChapterTracking = true; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata:  
   // For example: 3 chapters of 60 second duration each 
   
       var chapters:Vector.<VideoAnalyticsChapterData> = new Vector.<VideoAnalyticsChapterData>(); 
       var chapterDuration:int = 60; 
       for (var i:int = 0; i < 3; i++) { 
           var chapterData:VideoAnalyticsChapterData =  
             new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration); 
           chapterData.name = "chapter_%d" + (i+1); 
   
           chapters.push(chapterData); 
       } 
   
       vaMetadata.chapters = chapters; 
   
   // For default chapters, the application must not set custom chapters on the tracking metadata  
   // and simply enable chapters to be tracked by setting the boolean value as defined above. 
   ```

