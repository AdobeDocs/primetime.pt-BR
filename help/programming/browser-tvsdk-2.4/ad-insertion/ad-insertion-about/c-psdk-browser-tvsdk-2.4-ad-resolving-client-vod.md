---
description: Para conteúdo de vídeo sob demanda (VOD), o TVSDK do navegador insere quebras de publicidade ao vincular as publicidades no conteúdo principal para que a duração da linha do tempo aumente.
seo-description: Para conteúdo de vídeo sob demanda (VOD), o TVSDK do navegador insere quebras de publicidade ao vincular as publicidades no conteúdo principal para que a duração da linha do tempo aumente.
seo-title: VOD e resolução e inserção
title: VOD e resolução e inserção
uuid: 34a30ae5-d553-4c5d-9829-8e5eaa41c104
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# VOD e resolução e inserção{#vod-ad-resolving-and-insertion}

Para conteúdo de vídeo sob demanda (VOD), o TVSDK do navegador insere quebras de publicidade ao vincular as publicidades no conteúdo principal para que a duração da linha do tempo aumente.

Antes da reprodução, o TVSDK do navegador resolve anúncios conhecidos, insere e quebra no conteúdo principal, conforme descrito por uma linha do tempo retornada pela decisão do anúncio do Adobe Primetime, e recompata a linha do tempo virtual, se necessário.

O TVSDK do navegador insere anúncios das seguintes maneiras:

* **Pré-rolar**, que é anterior ao conteúdo.
* **Pós-rolagem**, que é após o conteúdo.

Após o início da reprodução, nenhuma alteração adicional pode ocorrer no conteúdo. Os anúncios não podem ser:

* Inserido
* Excluído

   Por exemplo, não é possível excluir anúncios integrados do conteúdo para oferecer uma experiência sem anúncios.
* Substituído

   Por exemplo, não é possível substituir anúncios incorporados por anúncios direcionados.

