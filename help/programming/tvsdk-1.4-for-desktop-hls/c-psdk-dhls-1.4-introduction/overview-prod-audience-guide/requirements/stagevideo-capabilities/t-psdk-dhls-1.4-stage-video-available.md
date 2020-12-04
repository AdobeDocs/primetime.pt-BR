---
description: Se StageVideo não estiver disponível e seu aplicativo tentar usar StageVideo, o TVSDK não emitirá um erro. Seu aplicativo pode determinar se o StageVideo está disponível ao acompanhar o StageVideoAvailabilityEvent.
seo-description: Se StageVideo não estiver disponível e seu aplicativo tentar usar StageVideo, o TVSDK não emitirá um erro. Seu aplicativo pode determinar se o StageVideo está disponível ao acompanhar o StageVideoAvailabilityEvent.
seo-title: Verifique se StageVideo está disponível
title: Verifique se StageVideo está disponível
uuid: 09c39442-cb9a-4892-af99-3d3d9bf1d4a7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 1%

---


# Verifique se StageVideo está disponível{#check-whether-stagevideo-is-available}

Se StageVideo não estiver disponível e seu aplicativo tentar usar StageVideo, o TVSDK não emitirá um erro. Seu aplicativo pode determinar se o StageVideo está disponível ao acompanhar o StageVideoAvailabilityEvent.

Do Flash 15 e posterior, quando o hardware `StageVideo` não estiver disponível, ele voltará para o software `StageVideo`. Para o Flash 14 e versões anteriores, você pode determinar se `StageVideo` está disponível. Se `StageVideo` não estiver disponível, você pode usar `StageVideoAvailabilityEvent` para entender por que ele não está disponível.

1. Escute `StageVideoAvailabilityEvent` para determinar se `StageVideo` está disponível.

   Por exemplo:

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. Se `StageVideo` não estiver disponível, marque `flash.media.StageVideoAvailabilityReason`.
