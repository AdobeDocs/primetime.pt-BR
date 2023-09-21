---
description: É possível inserir anúncios em VOD e conteúdo dinâmico/linear usando a interface de decisão de anúncios do Adobe Primetime. O Primetime Ad Decisioning trabalha com o TVSDK para identificar oportunidades de anúncios, resolver anúncios e inserir anúncios resolvidos em seus fluxos de vídeo.
title: Exigências para publicidade
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
