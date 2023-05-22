---
description: É possível inserir anúncios em VOD e conteúdo dinâmico/linear usando a interface de decisão de anúncios do Adobe Primetime.
title: Publicidade
exl-id: 79ee4abf-a3f5-4915-ad4b-fe866acec882
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Publicidade e seus requisitos {#advertising-requirements}

É possível inserir anúncios em VOD e conteúdo dinâmico/linear usando a interface de decisão de anúncios do Adobe Primetime.

O Primetime Ad Decisioning trabalha com o TVSDK para identificar oportunidades de anúncios, resolver anúncios e inserir anúncios resolvidos em seus fluxos de vídeo.

Para incorporar anúncios no seu conteúdo de vídeo, verifique se o conteúdo de publicidade e vídeo principal atende aos seguintes requisitos:

* A versão HLS do conteúdo de publicidade não pode ser superior à versão HLS do conteúdo principal.
* Os anúncios não precisam ser multiplexados (sem restrições), independentemente do conteúdo principal ser multiplexado.
