---
description: Para conteúdo VOD (Video-on-demand), o TVSDK insere quebras de publicidade ao dividir as publicidades no conteúdo principal para que a duração da linha do tempo aumente.
seo-description: Para conteúdo VOD (Video-on-demand), o TVSDK insere quebras de publicidade ao dividir as publicidades no conteúdo principal para que a duração da linha do tempo aumente.
seo-title: VOD e resolução e inserção
title: VOD e resolução e inserção
uuid: 33280792-ad08-41c1-b180-cc2159e8137c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# VOD e resolução e inserção{#vod-ad-resolving-and-insertion}

Para conteúdo VOD (Video-on-demand), o TVSDK insere quebras de publicidade ao dividir as publicidades no conteúdo principal para que a duração da linha do tempo aumente.

Antes da reprodução, o TVSDK resolve anúncios conhecidos, insere e quebra no conteúdo principal, conforme descrito por uma linha do tempo retornada pela decisão do anúncio do Adobe Primetime, e recompata a linha do tempo virtual, se necessário.

O TVSDK insere anúncios das seguintes maneiras:

* **Pré-rolar**, que é anterior ao conteúdo.
* **Meid-roll**, que está no conteúdo.
* **Pós-rolagem**, que é após o conteúdo.

Após o início da reprodução, nenhuma alteração adicional pode ocorrer no conteúdo. Os anúncios não podem ser:

* Inserido
* Excluído

   Por exemplo, não é possível excluir anúncios integrados do conteúdo para oferecer uma experiência sem anúncios.
* Substituído

   Por exemplo, não é possível substituir anúncios incorporados por anúncios direcionados.

