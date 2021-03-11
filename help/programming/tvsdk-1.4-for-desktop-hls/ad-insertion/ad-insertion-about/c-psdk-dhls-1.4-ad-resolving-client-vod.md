---
description: Para conteúdo de vídeo sob demanda (VOD), o TVSDK insere e quebra ao dividir os anúncios no conteúdo principal, de modo que a duração da linha do tempo aumente.
title: Resolução e inserção de anúncios VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Resolução e inserção de anúncios VOD{#vod-ad-resolving-and-insertion}

Para conteúdo de vídeo sob demanda (VOD), o TVSDK insere e quebra ao dividir os anúncios no conteúdo principal, de modo que a duração da linha do tempo aumente.

Antes da reprodução, o TVSDK resolve anúncios conhecidos, insere e quebra no conteúdo principal, conforme descrito por uma linha do tempo retornada de TVSDK, e recalcula a linha do tempo virtual, se necessário.

O TVSDK insere anúncios das seguintes maneiras:

* **Antes da exibição**, que é antes do conteúdo.
* **Mid-roll**, que está no conteúdo.
* **Pós-lançamento**, que é após o conteúdo.

>[!IMPORTANT]
>
>Ao implementar um `AdPolicySelector` personalizado, uma política diferente pode ser fornecida para cada tipo de `AdBreakTimelineItem` (precedente, intermediário ou posterior) em `AdPolicyInfo`, com base no tipo de `AdBreakTimelineItem`. Por exemplo, é possível manter o conteúdo intermediário após a reprodução, mas remover o conteúdo precedente após a reprodução.

Após o início da reprodução, nenhuma alteração adicional poderá ocorrer no conteúdo. Os anúncios não podem ser:

* Inserido
* Excluído

   Por exemplo, não é possível excluir anúncios integrados do conteúdo para oferecer uma experiência sem anúncios.
* Substituído

   Por exemplo, não é possível substituir anúncios incorporados por anúncios direcionados.

