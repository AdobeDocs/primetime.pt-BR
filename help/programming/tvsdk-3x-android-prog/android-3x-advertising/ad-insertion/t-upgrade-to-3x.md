---
description: 'A interface com.adobe.mediacore.timeline.TimelineMarker agora contém um novo método '
seo-description: 'A interface com.adobe.mediacore.timeline.TimelineMarker agora contém um novo método '
seo-title: 'Atualização de um anúncio com preguiça 2.5.x Resolvendo para solução de anúncios ociosa 3.0.0 (alterações na API/fluxo de trabalho) '
title: 'Atualização de um anúncio com preguiça 2.5.x Resolvendo para solução de anúncios ociosa 3.0.0 (alterações na API/fluxo de trabalho) '
uuid: 5870ceb4-93a8-4c8b-b716-673396122644
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Atualizando de um anúncio com preguiça 2.5.x Resolvendo para a Resolução de anúncios com preguiça 3.x (alterações de API/fluxo de trabalho):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

A interface com.adobe.mediacore.timeline.TimelineMarker agora contém um novo método:

**Placement.Type getPlacementType()**

Este método retornará um tipo de disposição de Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL ou Placement.Type.POST_ROLL. Se uma quebra de anúncio não for resolvida, o `getDuration()`método na interface do TimelineMarker retornará 0.

>[!NOTE]
>
>Essa interface nem sempre é convertida no tipo com.mediacore.timeline.advertit.AdBreakTimelineItem se ainda não tiver sido resolvida. Ele poderá ser aplicado se o `getDuration()` método do TimelineMarker for maior que 0.

**Alterações de evento:**

`kEventAdResolutionComplete` agora é depreciado e agora é acionado imediatamente após o player entrar no status PREPARADO. Os aplicativos que antes só escutavam esse evento para desenhar a barra de depuração devem alterá-la para `kEventTimelineUpdated` apenas ouvir. Depois que as pausas de anúncio individuais forem resolvidas, um novo `kEventTimelineUpdated` evento será despachado.
