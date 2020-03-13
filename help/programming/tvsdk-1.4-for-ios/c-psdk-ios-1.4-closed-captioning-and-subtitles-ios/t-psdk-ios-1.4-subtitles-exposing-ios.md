---
description: O TVSDK notifica o cliente do player sobre a disponibilidade de AVAsset's disponíveisMediaCharacteristicsWithMediaSelectionOptions internas usando a notificação PTMediaPlayerMediaSelectionOptionsAvailableNotification.
seo-description: O TVSDK notifica o cliente do player sobre a disponibilidade de AVAsset's disponíveisMediaCharacteristicsWithMediaSelectionOptions internas usando a notificação PTMediaPlayerMediaSelectionOptionsAvailableNotification.
seo-title: Expor legendas
title: Expor legendas
uuid: 657ab9c7-b205-4d13-81a7-51bc8e7d5ee2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Expor legendas {#expose-subtitles}

O TVSDK notifica o cliente do player sobre a disponibilidade de AVAsset&#39;s disponíveisMediaCharacteristicsWithMediaSelectionOptions internas usando a notificação PTMediaPlayerMediaSelectionOptionsAvailableNotification.

É possível acessar as legendas disponíveis por meio das `PTMediaPlayerItem` propriedades `subtitlesOptions`.

Para expor legendas:

1. Registre o cliente como um ouvinte para a `PTMediaPlayerMediaSelectionOptionsAvailableNotification` notificação.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   Quando o cliente recebe essa notificação, as legendas estão prontas no `PTMediaPlayerItem`.
1. Implemente o `onMediaPlayerItemMediaSelectionOptionsAvailable` método semelhante ao seguinte exemplo:

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   Para obter informações sobre faixas de áudio alternativas, consulte Áudio [](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md)alternativo.