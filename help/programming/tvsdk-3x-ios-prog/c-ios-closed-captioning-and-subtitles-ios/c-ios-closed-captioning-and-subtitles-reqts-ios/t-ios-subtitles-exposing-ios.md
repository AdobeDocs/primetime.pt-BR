---
description: O TVSDK notifica o cliente do reprodutor sobre a disponibilidade de AVAsset's availableMediaCharacteristicsWithMediaSelectionOptions internas usando a notificação PTMediaPlayerMediaSelectionOptionsAvailableNotification.
title: Expor legendas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Expor legendas {#expose-subtitles}

O TVSDK notifica o cliente do reprodutor sobre a disponibilidade de AVAsset&#39;s availableMediaCharacteristicsWithMediaSelectionOptions internas usando a notificação PTMediaPlayerMediaSelectionOptionsAvailableNotification.

Você pode acessar as legendas disponíveis por meio do `PTMediaPlayerItem` `subtitlesOptions` da propriedade.

Para expor legendas:

1. Registre o cliente como um ouvinte para a notificação `PTMediaPlayerMediaSelectionOptionsAvailableNotification`.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   Quando o cliente recebe essa notificação, as legendas estão prontas no `PTMediaPlayerItem`.
1. Implemente o método `onMediaPlayerItemMediaSelectionOptionsAvailable` semelhante ao seguinte exemplo:

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   Para obter informações sobre trilhas de áudio alternativas, consulte [Áudio alternativo](../../alternate-audio/ios-3x-alternate-audio.md).