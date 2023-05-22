---
description: A linha do tempo do anúncio adequada para uma reprodução de conteúdo de VOD pode ser inapropriada para reproduções subsequentes. É possível substituir uma linha do tempo de VOD sem alterar o conteúdo.
title: Alterações no VOD
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Alterações no VOD {#changes-to-vod}

A linha do tempo do anúncio adequada para uma reprodução de conteúdo de VOD pode ser inapropriada para reproduções subsequentes. É possível substituir uma linha do tempo de VOD sem alterar o conteúdo.

As situações em que convém substituir uma linha do tempo de VOD incluem:

* Substituir anúncios locais, mas deixar anúncios nacionais durante uma janela C3.
* Substitua os anúncios queimados após a janela C3 fechar.
* Substitua dinamicamente anúncios C3 antigos por anúncios mais novos e de maior duração.
* Insira menos anúncios ou nenhum anúncio.

É possível substituir a linha do tempo do anúncio enviando uma nova solicitação de inserção de anúncio com o arquivo M3U8 original e um valor diferente de `pttimeline` parâmetro de consulta.