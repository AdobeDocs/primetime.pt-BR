---
title: Implementar suporte de capítulo
description: Implementar suporte de capítulo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# Implementar suporte de capítulo {#implement-chapter-support}

Você pode definir e rastrear *personalizado* capítulos para rastreamento de vídeo em aplicativos baseados em TVSDK.

Os capítulos personalizados são gerenciados pelo aplicativo e se baseiam nos dados do CMS ou em outra forma que o aplicativo usa para definir capítulos.

>[!CAUTION]
>
>Os capítulos padrão não são compatíveis com o Android TVSDK 2.5.

1. Defina e acompanhe capítulos personalizados.

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
