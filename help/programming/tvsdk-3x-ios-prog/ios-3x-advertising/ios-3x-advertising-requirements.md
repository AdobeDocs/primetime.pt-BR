---
description: Você pode inserir anúncios no VOD e conteúdo ao vivo/linear usando a interface do Adobe Primetime Ad Decisioning.
title: Requisitos de publicidade
translation-type: tm+mt
source-git-commit: 944bfb0f3bd0050a9d2974a37f4fabddaaac8a93
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# Requisitos de publicidade {#advertising-requirements}

Você pode inserir anúncios no VOD e conteúdo ao vivo/linear usando a interface do Adobe Primetime Ad Decisioning.

<!--<a id="section_A2966DC850E140FE9400A1D9E412F819"></a>-->

O Primetime ad decisioning funciona com TVSDK para identificar oportunidades de anúncios, resolver anúncios e inserir anúncios resolvidos em seus fluxos de vídeo.

Para incorporar anúncios no seu conteúdo de vídeo, verifique se o anúncio e o conteúdo principal do vídeo atendem aos seguintes requisitos:

* A versão HLS do conteúdo de publicidade não pode ser superior à versão HLS do conteúdo principal.
* Os anúncios devem ser multiplexados e conter uma renderização somente de áudio, independentemente de o conteúdo principal ser multiplexado.
* As listas de reprodução de anúncio devem ter as mesmas representações de taxa de bits que as representações na lista de reprodução do conteúdo principal.
* A duração do target e a duração individual do fragmento de um anúncio não podem exceder a duração do target do conteúdo principal.
* Se o conteúdo principal contiver um fluxo somente de áudio, o conteúdo da publicidade também deverá conter um fluxo somente de áudio.
* Se o conteúdo principal contiver fluxos de subtítulo, o conteúdo da publicidade deverá ser descriptografado.
* Se o conteúdo principal for uma taxa de bits múltipla (MBR), o conteúdo do anúncio também deverá ser MBR.
* Se o conteúdo principal tiver trilhas de áudio alternativas, cada anúncio deve ter pelo menos um fluxo somente de áudio ou os anúncios devem ser descontinuados. Se o anúncio não tiver pelo menos um fluxo somente de áudio nem for descontinuado, o anúncio será ignorado.