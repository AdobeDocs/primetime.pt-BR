---
title: Implementar suporte de capítulo
description: Implementar suporte de capítulo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# Implementar suporte de capítulo{#implement-chapter-support}

Um capítulo é definido como o tempo entre cada ad break. Por exemplo, o tempo entre um ad break precedente e o primeiro mid-roll é definido como o primeiro capítulo. Você pode definir e rastrear capítulos para rastreamento de vídeo em um aplicativo com base no TVSDK do navegador usando capítulos personalizados. Os capítulos personalizados são gerenciados pelo aplicativo e se baseiam nos dados do CMS ou em outra forma que o aplicativo usa para definir capítulos.

1. Defina e acompanhe capítulos personalizados.

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
