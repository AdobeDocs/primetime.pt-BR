---
description: 'A interface com.adobe.mediacore.timeline.TimelineMarker agora contém um novo método '
title: 'Atualização da resolução de anúncios preguiçosos 2.5.x para a resolução de anúncios ociosos 3.0.0 (alterações de API/Fluxo de trabalho) '
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Atualização da resolução de anúncios preguiçosos 2.5.x para a resolução de anúncios ociosos 3.x (alterações de API/Fluxo de trabalho):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

A interface com.adobe.mediacore.timeline.TimelineMarker agora contém um novo método:

**Placement.Type getPlacementType()**

Este método retornará um tipo de disposição de Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL ou Placement.Type.POST_ROLL. Se um ad break não for resolvido, o método `getDuration()`na interface TimelineMarker retornará 0.

>[!NOTE]
>
>Essa interface nem sempre foi convertida no tipo com.mediacore.timeline.advertising.AdBreakTimelineItem se ainda não tiver sido resolvida. Ele poderá ser transmitido se o método `getDuration()` do TimelineMarker for maior que 0.

**Alterações no evento:**

`kEventAdResolutionComplete` agora é depreciado e acionado imediatamente após o reprodutor entrar no status PREPARED. Os aplicativos que anteriormente só escutavam esse evento para desenhar a barra de depuração devem alterá-la para escutar somente `kEventTimelineUpdated`. Depois que os ad breaks individuais forem resolvidos, um novo evento `kEventTimelineUpdated` será despachado.
