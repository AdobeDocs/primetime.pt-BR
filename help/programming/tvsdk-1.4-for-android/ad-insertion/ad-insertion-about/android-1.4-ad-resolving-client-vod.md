---
description: Para conteúdo de vídeo sob demanda (VOD), o TVSDK insere anúncios e os interrompe ao unir os anúncios no conteúdo principal para que a duração da linha do tempo aumente.
title: Resolução e inserção de anúncios de VOD
exl-id: 2e45fc35-85ca-4e34-b300-cf65878eeac6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# Resolução e inserção de anúncios de VOD{#vod-ad-resolving-and-insertion}

Para conteúdo de vídeo sob demanda (VOD), o TVSDK insere anúncios e os interrompe ao unir os anúncios no conteúdo principal para que a duração da linha do tempo aumente.

Antes de reproduzir, o TVSDK resolve anúncios conhecidos, insere ad breaks no conteúdo principal, conforme descrito por uma linha do tempo retornada do Adobe Primetime ad decisioning, e recalcula a linha do tempo virtual, se necessário.

O TVSDK insere anúncios das seguintes maneiras:

* **Antes da exibição**, que está antes do conteúdo.
* **Durante a exibição**, que está no conteúdo.
* **Pós-rolagem**, que está após o conteúdo.

Depois que a reprodução começa, nenhuma alteração adicional pode ocorrer no conteúdo. Os anúncios não podem ser:

* Inserido
* Excluído

   Por exemplo, não é possível excluir anúncios integrados do conteúdo para oferecer uma experiência sem anúncios.
* Substituído

   Por exemplo, não é possível substituir anúncios integrados por anúncios direcionados.
