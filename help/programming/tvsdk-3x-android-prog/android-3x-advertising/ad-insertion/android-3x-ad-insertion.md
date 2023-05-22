---
description: É possível inserir anúncios em VOD e conteúdo dinâmico/linear usando a interface de decisão de anúncios do Adobe Primetime. O Primetime Ad Decisioning trabalha com o TVSDK para identificar oportunidades de anúncios, resolver anúncios e inserir anúncios resolvidos em seus fluxos de vídeo.
title: Exigências para publicidade
exl-id: 3ca82cc5-ed64-458e-9a8d-475a84512478
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Publicidade e seus requisitos {#advertising-requirements}

É possível inserir anúncios em VOD e conteúdo dinâmico/linear usando a interface de decisão de anúncios do Adobe Primetime. O Primetime Ad Decisioning trabalha com o TVSDK para identificar oportunidades de anúncios, resolver anúncios e inserir anúncios resolvidos em seus fluxos de vídeo.

<!--<a id="section_282A8000A8BF4860A24F0D3F1A19BC9E"></a>-->

Para incorporar anúncios no seu conteúdo de vídeo, verifique se o conteúdo de publicidade e vídeo principal atende aos seguintes requisitos:

* A versão HLS do conteúdo de publicidade não pode ser superior à versão HLS do conteúdo principal.
* Os anúncios não precisam ser multiplexados (sem restrições), independentemente do conteúdo principal ser multiplexado.
