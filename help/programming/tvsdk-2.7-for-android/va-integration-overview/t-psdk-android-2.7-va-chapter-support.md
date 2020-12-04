---
description: nulo
seo-description: nulo
seo-title: Implementar suporte a capítulo
title: Implementar suporte a capítulo
uuid: f62a8244-6393-4a38-9ae2-8ac31f6a8a06
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# Implementar o suporte de capítulo {#implement-chapter-support}

Você pode definir e rastrear *capítulos personalizados* para rastreamento de vídeo em aplicativos baseados em TVSDK.

Os capítulos personalizados são gerenciados pelo aplicativo e são baseados nos dados do CMS ou de outra forma que o aplicativo usa para definir capítulos.

>[!CAUTION]
>
>Os capítulos padrão não são suportados no Android TVSDK 2.5.

1. Defina e rastreie capítulos personalizados.

   ```java
   // First, enable chapter tracking by setting   
   // enableChapterTracking to true: 
   
   vaMetadata.enableChapterTracking(true); 
   // For custom chapter definitions, provide  
   // an array list of chapters through the metadata. 
   // For example: 3 chapters of 60 second duration each 
   
   List<VideoAnalyticsChapterData> chapters =  
     new ArrayList<VideoAnalyticsChapterData>(); 
   
   Int chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       VideoAnalyticsChapterData chapterData =  
         new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration);  
       chapterData.setName("chapter_" + (i+1)); 
       chapters.add(chapterData); 
   } 
   
   vaMetadata.setChapters(chapters); 
   ```

