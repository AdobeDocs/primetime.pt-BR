---
description: Se StageVideo não estiver disponível e o aplicativo tentar usar StageVideo, o TVSDK não emitirá um erro. Seu aplicativo pode determinar se StageVideo está disponível ouvindo StageVideoAvailabilityEvent.
title: Verifique se StageVideo está disponível
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---


# Verifique se StageVideo está disponível{#check-whether-stagevideo-is-available}

Se StageVideo não estiver disponível e o aplicativo tentar usar StageVideo, o TVSDK não emitirá um erro. Seu aplicativo pode determinar se StageVideo está disponível ouvindo StageVideoAvailabilityEvent.

A partir do Flash 15 e posterior, quando o hardware `StageVideo` não estiver disponível, ele voltará para o software `StageVideo`. Para o Flash 14 e anterior, você pode determinar se `StageVideo` está disponível. Se `StageVideo` não estiver disponível, você poderá usar `StageVideoAvailabilityEvent` para entender por que ele não está disponível.

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
