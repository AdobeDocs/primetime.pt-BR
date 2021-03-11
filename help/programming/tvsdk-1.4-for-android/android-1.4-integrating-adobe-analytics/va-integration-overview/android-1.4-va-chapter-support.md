---
title: Implementar o suporte ao capítulo
description: Implementar o suporte ao capítulo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Implementar o suporte a capítulo {#implement-chapter-support}

Você pode definir e rastrear capítulos para rastreamento de vídeo em um aplicativo baseado em TVSDK das seguintes maneiras:

* Capítulos padrão, que são gerenciados internamente pelo TVSDK.

   Um capítulo é definido como o tempo entre cada ad break. Por exemplo, o tempo entre um ad break precedente e o primeiro intermediário é definido como o primeiro capítulo.
* Capítulos personalizados, que são gerenciados pelo aplicativo e se baseiam em dados CMS ou em outra maneira que o aplicativo usa para definir capítulos.

1. Defina e rastreie capítulos padrão ou personalizados.

   ```java
   // First, enable chapter tracking by setting  
   // the Boolean 'enableChapterTracking' to true: 
   
   vaMetadata.enableChapterTracking(true); 
   // For custom chapter definitions, provide an array list of chapters  
   // through the metadata. 
   // For example: 3 chapters of 60 second duration each 
   
   List<VideoAnalyticsChapterData> chapters = new ArrayList<VideoAnalyticsChapterData>(); 
   
   Int chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       VideoAnalyticsChapterData chapterData =  
         new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration);  
       chapterData.setName("chapter_" + (i+1)); 
       chapters.add(chapterData); 
   } 
   
   vaMetadata.setChapters(chapters); 
   // For default chapters, the application must not set  
   // custom chapters on the tracking metadata 
   // and simply enable chapters to be tracked by setting  
   // the boolean value as defined above.
   ```
