---
description: Para conteúdo de vídeo sob demanda (VOD), o TVSDK insere anúncios e os interrompe ao unir os anúncios no conteúdo principal para que a duração da linha do tempo aumente.
title: Resolução e inserção de anúncios de VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Resolução e inserção de anúncios de VOD{#vod-ad-resolving-and-insertion}

Para conteúdo de vídeo sob demanda (VOD), o TVSDK insere anúncios e os interrompe ao unir os anúncios no conteúdo principal para que a duração da linha do tempo aumente.

Antes de reproduzir, o TVSDK resolve anúncios conhecidos, insere ad breaks no conteúdo principal, conforme descrito por uma linha do tempo retornada do TVSDK, e recalcula a linha do tempo virtual, se necessário.

O TVSDK insere anúncios das seguintes maneiras:

* **Antes da exibição**, que está antes do conteúdo.
* **Durante a exibição**, que está no conteúdo.
* **Pós-rolagem**, que está após o conteúdo.

>[!IMPORTANT]
>
>Ao implementar uma `AdPolicySelector`, uma política diferente pode ser aplicada a cada tipo de `AdBreakTimelineItem` (antes da exibição, durante ou após a exibição) em `AdPolicyInfo`, com base no tipo de `AdBreakTimelineItem`. Por exemplo, você pode manter o conteúdo durante a exibição após sua reprodução, mas remover o conteúdo anterior à exibição após sua reprodução.

Depois que a reprodução começa, nenhuma alteração adicional pode ocorrer no conteúdo. Os anúncios não podem ser:

* Inserido
* Excluído

  Por exemplo, não é possível excluir anúncios integrados do conteúdo para oferecer uma experiência sem anúncios.
* Substituído

  Por exemplo, não é possível substituir anúncios integrados por anúncios direcionados.
