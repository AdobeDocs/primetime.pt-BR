---
description: Para conteúdo de vídeo sob demanda (VOD), o TVSDK insere anúncios e os interrompe ao unir os anúncios no conteúdo principal para que a duração da linha do tempo aumente.
title: Resolver e inserir anúncio de VOD
exl-id: c8e1423c-5d53-452c-ad01-8335ccf42471
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Resolver e inserir anúncios de VOD {#resolve-and-insert-vod-ad}

Para conteúdo de vídeo sob demanda (VOD), o TVSDK insere anúncios e os interrompe ao unir os anúncios no conteúdo principal para que a duração da linha do tempo aumente.

Antes de reproduzir, o TVSDK resolve anúncios conhecidos, insere ad breaks no conteúdo principal, conforme descrito por uma linha do tempo retornada do Adobe Primetime ad decisioning, e recalcula a linha do tempo virtual, se necessário.

O TVSDK insere anúncios das seguintes maneiras:

* **Antes da exibição**, que é colocado antes do conteúdo.
* **Durante a exibição**, que está no meio do conteúdo.
* **Pós-rolagem**, que é colocado depois do conteúdo.

>[!TIP]
>
>Depois que a reprodução começa, nenhuma alteração adicional pode ocorrer no conteúdo.

Os anúncios não podem ser:

* Inserido
* Excluído

   Por exemplo, não é possível excluir anúncios integrados do conteúdo para oferecer uma experiência sem anúncios.
* Substituído

   Por exemplo, não é possível substituir anúncios integrados por anúncios direcionados.
