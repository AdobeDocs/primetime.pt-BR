---
title: Implementar o suporte ao capítulo
description: Implementar o suporte ao capítulo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---


# Implementar o suporte a capítulo {#implement-chapter-support}

Você pode definir e rastrear capítulos *personalizados* para rastreamento de vídeo em aplicativos baseados em TVSDK.

Os capítulos personalizados são gerenciados pelo aplicativo e se baseiam em dados CMS ou em outra maneira que o aplicativo usa para definir capítulos.

>[!CAUTION]
>
>Os capítulos padrão não são compatíveis com o Android TVSDK 3.0.

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
