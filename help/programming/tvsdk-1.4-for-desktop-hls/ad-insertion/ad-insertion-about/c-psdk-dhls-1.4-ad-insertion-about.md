---
description: A inserção de anúncio resolve os anúncios de VOD (video-on-demand) , para transmissão ao vivo e para transmissão linear com rastreamento de anúncios e reprodução de anúncios. O TVSDK faz as solicitações necessárias para o servidor de publicidade, recebe informações sobre anúncios para o conteúdo especificado e coloca os anúncios em fases.
title: Inserção de anúncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---


# Visão geral {#inserting-ads-overview}

A inserção de anúncio resolve os anúncios de VOD (video-on-demand) , para transmissão ao vivo e para transmissão linear com rastreamento de anúncios e reprodução de anúncios. O TVSDK faz as solicitações necessárias para o servidor de publicidade, recebe informações sobre anúncios para o conteúdo especificado e coloca os anúncios em fases.

Um *`ad break`* contém um ou mais anúncios que são exibidos em sequência. O TVSDK insere anúncios no conteúdo principal como membros de um ou mais ad breaks.

## Desativar anúncios precedentes {#disable-preroll-ads}

Para desativar o anúncio antes da exibição, altere os geradores de oportunidade padrão para não fazer a chamada antes da exibição. Os geradores de oportunidade padrão são:

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
result.push(new AdSignalingModeOpportunityGenerator()); 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```

Para desativar o precedente em fluxos ao vivo, altere o acima para incluir somente SpliceOutOpportunityGenerator:

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
if (preroll_enabled == true) { result.push(new AdSignalingModeOpportunityGenerator()); } 
 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```
