---
description: A inserção de anúncios resolve os anúncios para vídeo sob demanda (VOD), para transmissão ao vivo e para transmissão linear com rastreamento de anúncios e reprodução de anúncios. O TVSDK faz as solicitações necessárias para o servidor de anúncios, recebe informações sobre anúncios para o conteúdo especificado e coloca os anúncios no conteúdo em fases.
seo-description: A inserção de anúncios resolve os anúncios para vídeo sob demanda (VOD), para transmissão ao vivo e para transmissão linear com rastreamento de anúncios e reprodução de anúncios. O TVSDK faz as solicitações necessárias para o servidor de anúncios, recebe informações sobre anúncios para o conteúdo especificado e coloca os anúncios no conteúdo em fases.
seo-title: Inserir anúncios
title: Inserir anúncios
uuid: 25c79822-a861-427b-b6a8-24714b21aae4
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Visão geral {#inserting-ads-overview}

A inserção de anúncios resolve os anúncios para vídeo sob demanda (VOD), para transmissão ao vivo e para transmissão linear com rastreamento de anúncios e reprodução de anúncios. O TVSDK faz as solicitações necessárias para o servidor de anúncios, recebe informações sobre anúncios para o conteúdo especificado e coloca os anúncios no conteúdo em fases.

Um *`ad break`* contém uma ou mais publicidades que são reproduzidas em sequência. O TVSDK insere publicidades no conteúdo principal como membros de uma ou mais pausas de publicidade.

## Desativar anúncios precedentes {#disable-preroll-ads}

Para desativar a pre-roll, altere os geradores de oportunidade padrão para não fazer a chamada pré-roll. Os geradores de oportunidade padrão são:

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

Para desativar a pré-rolagem em fluxos ao vivo, altere as opções acima para incluir somente o SpliceOutOpportunityGenerator:

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
