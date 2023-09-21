---
description: A interface com.adobe.mediacore.timeline.TimelineMarker agora contém um novo método
title: Atualização da Resolução de anúncio lento 2.5.x para Resolução de anúncio lento 3.0.0 (alterações na API/fluxo de trabalho)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Atualização da Resolução de anúncio lento 2.5.x para Resolução de anúncio lento 3.x (alterações na API/fluxo de trabalho):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

A interface com.adobe.mediacore.timeline.TimelineMarker agora contém um novo método:

**Placement.Type getPlacementType()**

Esse método retornará um tipo de posicionamento de Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL ou Placement.Type.POST_ROLL. Se um ad break não for resolvido, a variável `getDuration()`na interface do TimelineMarker retornará 0.

>[!NOTE]
>
>Essa interface nem sempre é convertida no tipo com.mediacore.timeline.advertising.AdBreakTimelineItem se ainda não tiver sido resolvida. Ele poderá ser lançado se a variável `getDuration()` O método TimelineMarker é maior que 0.

**Alterações no evento:**

`kEventAdResolutionComplete` O agora é depreciado e acionado imediatamente após o player entrar no status PREPARADO. Os aplicativos que anteriormente só ouviam esse evento para desenhar a barra de depuração devem alterar isso para ouvir `kEventTimelineUpdated` somente. Depois que ad breaks individuais forem resolvidos, um novo `kEventTimelineUpdated` evento será despachado.
