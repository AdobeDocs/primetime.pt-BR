---
description: O TVSDK notifica o cliente do player sobre a disponibilidade de AVAsset's disponíveisMediaCharacteristicsWithMediaSelectionOptions internas usando a notificação PTMediaPlayerMediaSelectionOptionsAvailableNotification.
seo-description: O TVSDK notifica o cliente do player sobre a disponibilidade de AVAsset's disponíveisMediaCharacteristicsWithMediaSelectionOptions internas usando a notificação PTMediaPlayerMediaSelectionOptionsAvailableNotification.
seo-title: Expor legendas
title: Expor legendas
uuid: 1cd8761f-6e6f-4017-9852-fa61f36197c5
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

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

   Para obter informações sobre faixas de áudio alternativas, consulte Áudio [](../../alternate-audio/ios-3x-alternate-audio.md)alternativo.