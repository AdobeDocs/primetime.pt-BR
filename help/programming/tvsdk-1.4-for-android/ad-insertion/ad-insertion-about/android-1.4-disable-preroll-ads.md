---
title: Desativar anúncios precedentes
description: Desativar anúncios precedentes
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 0%

---


# Desativar anúncios precedentes{#disable-pre-roll-ads}

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

