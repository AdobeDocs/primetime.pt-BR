---
description: A linha do tempo do anúncio apropriada para uma reprodução do conteúdo de VOD pode ser inadequada para reproduções subsequentes. Você pode substituir uma linha do tempo de VOD sem alterar o conteúdo.
title: Alterações no VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Alterações no VOD {#changes-to-vod}

A linha do tempo do anúncio apropriada para uma reprodução do conteúdo de VOD pode ser inadequada para reproduções subsequentes. Você pode substituir uma linha do tempo de VOD sem alterar o conteúdo.

As situações nas quais você pode substituir uma linha do tempo VOD incluem:

* Substitua anúncios locais, mas deixe anúncios nacionais durante uma janela C3.
* Substitua os anúncios queimados depois que a janela C3 for fechada.
* Substitua dinamicamente anúncios C3 antigos por anúncios mais recentes de maior duração.
* Inserir menos anúncios ou nenhum.

Você pode substituir a linha do tempo do anúncio enviando uma nova solicitação de inserção de anúncio com o arquivo M3U8 original e um valor diferente do parâmetro de consulta `pttimeline`.