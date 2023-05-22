---
description: Se o StageVideo não estiver disponível e seu aplicativo tentar usar o StageVideo, o TVSDK não emitirá um erro. O aplicativo pode determinar se o StageVideo está disponível ouvindo StageVideoAvailabilityEvent.
title: Verificar se StageVideo está disponível
exl-id: 24136a14-8d7d-4569-9911-fac4e2de3227
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# Verificar se StageVideo está disponível{#check-whether-stagevideo-is-available}

Se o StageVideo não estiver disponível e seu aplicativo tentar usar o StageVideo, o TVSDK não emitirá um erro. O aplicativo pode determinar se o StageVideo está disponível ouvindo StageVideoAvailabilityEvent.

Do Flash 15 e posterior, quando o hardware `StageVideo` não estiver disponível, recorrerá ao software `StageVideo`. Para o Flash 14 e anterior, você pode determinar se `StageVideo` está disponível. Se `StageVideo` não estiver disponível, você poderá usar `StageVideoAvailabilityEvent` para entender por que ele não está disponível.

1. Ouvir `StageVideoAvailabilityEvent` para determinar se `StageVideo` está disponível.

   Por exemplo:

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. Se `StageVideo` não estiver disponível, marque `flash.media.StageVideoAvailabilityReason`.
