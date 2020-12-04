---
description: Você pode fornecer metadados personalizados sobre conteúdo, anúncios e chamadas de rastreamento de capítulo usando funções de retorno de chamada.
seo-description: Você pode fornecer metadados personalizados sobre conteúdo, anúncios e chamadas de rastreamento de capítulo usando funções de retorno de chamada.
seo-title: Implementação do suporte a metadados personalizados
title: Implementação do suporte a metadados personalizados
uuid: 6e23311c-a393-4485-919e-4cf6412789b1
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# Implementação do suporte a metadados personalizados{#implement-custom-metadata-support}

Você pode fornecer metadados personalizados sobre conteúdo, anúncios e chamadas de rastreamento de capítulo usando funções de retorno de chamada.

As funções de retorno de chamada são chamadas logo antes da chamada de rastreamento ser feita, de modo que seu aplicativo possa anexar os metadados específicos a um anúncio ou capítulo.

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

