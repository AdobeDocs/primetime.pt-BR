---
description: A linha do tempo do anúncio apropriada para uma reprodução do conteúdo VOD pode ser inadequada para reproduções subsequentes. É possível substituir uma linha do tempo VOD sem alterar o conteúdo.
seo-description: A linha do tempo do anúncio apropriada para uma reprodução do conteúdo VOD pode ser inadequada para reproduções subsequentes. É possível substituir uma linha do tempo VOD sem alterar o conteúdo.
seo-title: Alterações no VOD
title: Alterações no VOD
uuid: e734aacd-b42e-4c8e-a16a-c7a0739a0492
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Alterações no VOD {#changes-to-vod}

A linha do tempo do anúncio apropriada para uma reprodução do conteúdo VOD pode ser inadequada para reproduções subsequentes. É possível substituir uma linha do tempo VOD sem alterar o conteúdo.

As situações nas quais você pode substituir uma linha do tempo VOD incluem:

* Substitua os anúncios locais, mas deixe os anúncios nacionais durante uma janela C3.
* Substitua os anúncios queimados depois que a janela C3 for fechada.
* Substitua dinamicamente anúncios C3 antigos por anúncios mais recentes de maior duração.
* Inserir menos anúncios ou nenhum anúncio.

Você pode substituir a linha do tempo do anúncio enviando uma nova solicitação de inserção de publicidade ao arquivo M3U8 original e um valor diferente do parâmetro do query `pttimeline`.