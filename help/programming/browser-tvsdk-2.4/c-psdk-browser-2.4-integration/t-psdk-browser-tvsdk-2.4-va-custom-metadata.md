---
description: Você pode fornecer metadados personalizados sobre conteúdo, anúncios e chamadas de rastreamento de capítulo usando funções de retorno de chamada.
title: Implementar suporte a metadados personalizados
exl-id: d2291649-79e2-4935-8980-4f2038d58342
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# Implementar suporte a metadados personalizados{#implement-custom-metadata-support}

Você pode fornecer metadados personalizados sobre conteúdo, anúncios e chamadas de rastreamento de capítulo usando funções de retorno de chamada.

As funções de retorno de chamada são chamadas antes da chamada de rastreamento ser feita, para que o aplicativo possa anexar os metadados específicos a um anúncio ou capítulo.

1. Chame funções de retorno de chamada para conteúdo, anúncios e capítulos.

   ```js
   vaObj.videoMetadataBlock = function() { 
       return { 
           "name" : "my-video", 
           "genre" : "comedy" 
       }; 
   } 
   
   vaObj.adMetadataBlock = function(ad) { 
       return { 
           "name" : "my-ad", 
           "category" : "automotive" 
       }; 
   } 
   
   vaObj.chapterMetadataBlock = function(chapter) { 
       return { 
           "name" : "my-chapter", 
           "type" : "quartile" 
       }; 
   }
   ```
