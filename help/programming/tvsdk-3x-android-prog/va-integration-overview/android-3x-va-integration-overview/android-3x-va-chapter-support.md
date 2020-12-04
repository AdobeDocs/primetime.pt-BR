---
description: nulo
seo-description: nulo
seo-title: Implementar suporte a capítulo
title: Implementar suporte a capítulo
uuid: 6e2c3994-d28b-489f-ae60-9b876125a871
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# Implementar o suporte de capítulo {#implement-chapter-support}

Você pode definir e rastrear *capítulos personalizados* para rastreamento de vídeo em aplicativos baseados em TVSDK.

Os capítulos personalizados são gerenciados pelo aplicativo e são baseados nos dados do CMS ou de outra forma que o aplicativo usa para definir capítulos.

>[!CAUTION]
>
>Os capítulos padrão não são suportados no Android TVSDK 3.0.

Defina e rastreie capítulos personalizados.

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
