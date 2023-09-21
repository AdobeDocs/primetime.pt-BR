---
description: A inserção de anúncios soluciona anúncios de VOD (Video On Demand, vídeo sob demanda), de transmissão ao vivo e de transmissão linear com rastreamento de anúncios e reprodução de anúncio. O TVSDK faz as solicitações necessárias ao servidor de anúncios, recebe informações sobre os anúncios do conteúdo especificado e coloca os anúncios no conteúdo em fases.
title: Inserção de anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# Visão geral {#inserting-ads-overview}

A inserção de anúncios soluciona anúncios de VOD (Video On Demand, vídeo sob demanda), de transmissão ao vivo e de transmissão linear com rastreamento de anúncios e reprodução de anúncio. O TVSDK faz as solicitações necessárias ao servidor de anúncios, recebe informações sobre os anúncios do conteúdo especificado e coloca os anúncios no conteúdo em fases.

Um *`ad break`* contém um ou mais anúncios reproduzidos em sequência. O TVSDK insere anúncios no conteúdo principal como membros de um ou mais ad breaks.

## Desativar anúncios precedentes {#disable-preroll-ads}

Para desativar o antes da exibição, altere os geradores de oportunidade padrão para não fazer a chamada antes da exibição. Os geradores de oportunidade padrão são:

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

Para desabilitar a pré-implantação em fluxos ao vivo, altere o acima para incluir somente o SpliceOutOpportunityGenerator:

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
