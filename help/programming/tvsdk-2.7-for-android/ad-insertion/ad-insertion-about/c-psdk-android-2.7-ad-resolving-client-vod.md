---
description: Para conteúdo de vídeo sob demanda (VOD), o TVSDK insere e quebra ao dividir os anúncios no conteúdo principal, de modo que a duração da linha do tempo aumente.
title: Resolver e inserir anúncio VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Resolver e inserir anúncios VOD {#resolve-and-insert-vod-ad}

Para conteúdo de vídeo sob demanda (VOD), o TVSDK insere e quebra ao dividir os anúncios no conteúdo principal, de modo que a duração da linha do tempo aumente.

Antes da reprodução, o TVSDK resolve anúncios conhecidos, insere e quebra no conteúdo principal, conforme descrito por uma linha do tempo retornada pela decisão do anúncio do Adobe Primetime, e recalcula a linha do tempo virtual, se necessário.

O TVSDK insere anúncios das seguintes maneiras:

* **Antes da exibição**, que é colocada antes do conteúdo.
* **Meio**, que está no meio do conteúdo.
* **Pós-rolo**, que é colocado depois do conteúdo.

>[!TIP]
>
>Após o início da reprodução, nenhuma alteração adicional poderá ocorrer no conteúdo.

Os anúncios não podem ser:

* Inserido
* Excluído

   Por exemplo, não é possível excluir anúncios integrados do conteúdo para oferecer uma experiência sem anúncios.
* Substituído

   Por exemplo, não é possível substituir anúncios incorporados por anúncios direcionados.

