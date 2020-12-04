---
description: nulo
seo-description: nulo
seo-title: Implementar suporte a capítulo
title: Implementar suporte a capítulo
uuid: 70f10621-febe-4443-84e7-ce95bec53377
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# Implementar suporte a capítulo{#implement-chapter-support}

Um capítulo é definido como o tempo entre cada intervalo de anúncios. Por exemplo, o tempo entre uma pausa de anúncio precedente e o primeiro intermediário é definido como o primeiro capítulo. Você pode definir e rastrear capítulos para rastreamento de vídeo em um aplicativo baseado em TVSDK do navegador usando capítulos personalizados. Os capítulos personalizados são gerenciados pelo aplicativo e são baseados em dados CMS ou de outra forma que o aplicativo usa para definir capítulos.

1. Defina e rastreie capítulos personalizados.

   ```js
   vaObj.enableChapterTracking = true; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata: 
   // For example: 3 chapters of 60 second duration each 
   var chapters = []; 
   var chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       var chapterData = new AdobePSDK.VA.VideoAnalyticsChapterData("chapter_" + (i+1), i * chapterDuration, chapterDuration, (i+1)); 
       chapters.push(chapterData); 
   } 
   
   vaObj.chapters = chapters;
   ```

