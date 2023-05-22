---
title: Exigências para publicidade
description: Exigências para publicidade
copied-description: true
exl-id: 906f4910-396c-4909-8e22-119486ed13a0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Exigências para publicidade {#advertising-requirements}

É possível inserir anúncios em VOD e conteúdo dinâmico/linear usando a interface de decisão de anúncios do Adobe Primetime.

O Primetime Ad Decisioning funciona com TVSDK para identificar oportunidades de anúncios, resolver anúncios e inserir anúncios resolvidos em seus fluxos de vídeo.

Para incorporar anúncios no seu conteúdo de vídeo, verifique se o conteúdo de publicidade e vídeo principal atende aos seguintes requisitos:

* A versão HLS do conteúdo de publicidade não pode ser superior à versão HLS do conteúdo principal.
* Os anúncios devem ser multiplexados e devem conter uma representação somente de áudio, independentemente do conteúdo principal ser multiplexado.
* As listas de reprodução de anúncios devem ter as mesmas representações de taxa de bits que as representações na lista de reprodução do conteúdo principal.
* A duração alvo e a duração de fragmento individual de um anúncio não podem exceder a duração alvo do conteúdo principal.
* Se o conteúdo principal contiver um fluxo somente de áudio, o conteúdo de publicidade também deverá conter um fluxo somente de áudio.
* Se o conteúdo principal contiver fluxos de legendas, o conteúdo de publicidade deve ser descriptografado.
* Se o conteúdo principal for MBR (multiple bit rate), o conteúdo de publicidade também deverá ser MBR.
* Se o conteúdo principal tiver faixas de áudio alternativas, cada anúncio deve ter pelo menos um fluxo somente de áudio.

   Se o anúncio não tiver pelo menos um fluxo somente de áudio, o anúncio será ignorado.
