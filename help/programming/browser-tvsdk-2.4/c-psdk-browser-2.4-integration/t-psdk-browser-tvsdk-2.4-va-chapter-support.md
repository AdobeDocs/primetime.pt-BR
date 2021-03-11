---
title: Implementar o suporte ao capítulo
description: Implementar o suporte ao capítulo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---


# Implementar o suporte a capítulo{#implement-chapter-support}

Um capítulo é definido como o tempo entre cada ad break. Por exemplo, o tempo entre um ad break precedente e o primeiro intermediário é definido como o primeiro capítulo. Você pode definir e rastrear capítulos para rastreamento de vídeo em um aplicativo baseado em TVSDK do navegador usando capítulos personalizados. Os capítulos personalizados são gerenciados pelo aplicativo e se baseiam em dados CMS ou em outra maneira que o aplicativo usa para definir capítulos.

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

