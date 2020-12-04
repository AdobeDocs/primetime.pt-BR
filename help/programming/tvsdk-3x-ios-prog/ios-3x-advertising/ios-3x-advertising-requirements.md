---
description: Você pode inserir publicidades em seu VOD e conteúdo ao vivo/linear usando a interface de decisão de publicidade da Adobe Primetime.
seo-description: Você pode inserir publicidades em seu VOD e conteúdo ao vivo/linear usando a interface de decisão de publicidade da Adobe Primetime.
seo-title: Requisitos de publicidade
title: Requisitos de publicidade
uuid: 0287f1e4-746f-42e5-b811-409064dd9b13
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Requisitos de publicidade {#advertising-requirements}

Você pode inserir publicidades em seu VOD e conteúdo ao vivo/linear usando a interface de decisão de publicidade da Adobe Primetime.

<!--<a id="section_A2966DC850E140FE9400A1D9E412F819"></a>-->

A decisão do anúncio Primetime funciona com o TVSDK para identificar oportunidades de anúncios, resolver anúncios e inserir anúncios resolvidos em seus fluxos de vídeo.

Para incorporar anúncios ao seu conteúdo de vídeo, certifique-se de que a publicidade e o conteúdo de vídeo principal atendam aos seguintes requisitos:

* A versão HLS do conteúdo de publicidade não pode ser superior à versão HLS do conteúdo principal.
* Os anúncios devem ser multiplexados e conter uma execução somente de áudio, independentemente de o conteúdo principal ser multiplexado.
* As listas de reprodução do anúncio devem ter as mesmas execuções de taxa de bits que as execuções na lista de reprodução do conteúdo principal.
* A duração do público alvo e a duração do fragmento individual de um anúncio não podem exceder a duração do público alvo do conteúdo principal.
* Se o conteúdo principal contiver um fluxo somente de áudio, o conteúdo de publicidade também deverá conter um fluxo somente de áudio.
* Se o conteúdo principal contiver fluxos de legendas, o conteúdo do anúncio deverá ser não criptografado.
* Se o conteúdo principal for uma taxa de bits múltipla (MBR), o conteúdo do anúncio também deverá ser MBR.
* Se o conteúdo principal tiver faixas de áudio alternativas, cada anúncio deve ter pelo menos um fluxo somente de áudio.

Se o anúncio não tiver pelo menos um fluxo somente de áudio, ele será ignorado.