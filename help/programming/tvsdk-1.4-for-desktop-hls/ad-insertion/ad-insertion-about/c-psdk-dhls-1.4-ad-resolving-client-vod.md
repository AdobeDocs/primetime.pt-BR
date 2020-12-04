---
description: Para conteúdo VOD (Video-on-demand), o TVSDK insere quebras de publicidade ao dividir as publicidades no conteúdo principal para que a duração da linha do tempo aumente.
seo-description: Para conteúdo VOD (Video-on-demand), o TVSDK insere quebras de publicidade ao dividir as publicidades no conteúdo principal para que a duração da linha do tempo aumente.
seo-title: VOD e resolução e inserção
title: VOD e resolução e inserção
uuid: c1017483-5b4f-4d71-9589-fb2327b4572b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Resolução e inserção de anúncio VOD{#vod-ad-resolving-and-insertion}

Para conteúdo VOD (Video-on-demand), o TVSDK insere quebras de publicidade ao dividir as publicidades no conteúdo principal para que a duração da linha do tempo aumente.

Antes da reprodução, o TVSDK resolve os anúncios conhecidos, insere e quebra no conteúdo principal, conforme descrito por uma linha do tempo retornada do TVSDK, e recompata a linha do tempo virtual, se necessário.

O TVSDK insere anúncios das seguintes maneiras:

* **Pré-rolar**, que é anterior ao conteúdo.
* **Meid-roll**, que está no conteúdo.
* **Pós-rolagem**, que é após o conteúdo.

>[!IMPORTANT]
>
>Ao implementar um `AdPolicySelector` personalizado, uma política diferente pode ser fornecida para cada tipo de `AdBreakTimelineItem` (pre-roll, mid-roll ou post-roll) em `AdPolicyInfo`, com base no tipo de `AdBreakTimelineItem`. Por exemplo, você pode manter o conteúdo intermediário após a reprodução, mas remover o conteúdo anterior à reprodução depois que ele for reproduzido.

Após os start de reprodução, nenhuma alteração adicional pode ocorrer no conteúdo. Os anúncios não podem ser:

* Inserido
* Excluído

   Por exemplo, não é possível excluir anúncios integrados do conteúdo para oferta de uma experiência sem anúncios.
* Substituído

   Por exemplo, não é possível substituir anúncios incorporados por anúncios direcionados.

