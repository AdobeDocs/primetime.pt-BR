---
description: O TVSDK notifica o cliente do player sobre a disponibilidade de AVAsset's disponíveisMediaCharacteristicsWithMediaSelectionOptions internas usando a notificação PTMediaPlayerMediaSelectionOptionsAvailableNotification.
seo-description: O TVSDK notifica o cliente do player sobre a disponibilidade de AVAsset's disponíveisMediaCharacteristicsWithMediaSelectionOptions internas usando a notificação PTMediaPlayerMediaSelectionOptionsAvailableNotification.
seo-title: Expor legendas
title: Expor legendas
uuid: 657ab9c7-b205-4d13-81a7-51bc8e7d5ee2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Expor legendas {#expose-subtitles}

O TVSDK notifica o cliente do player sobre a disponibilidade de AVAsset&#39;s disponíveisMediaCharacteristicsWithMediaSelectionOptions internas usando a notificação PTMediaPlayerMediaSelectionOptionsAvailableNotification.

Você pode acessar as legendas disponíveis por meio das `PTMediaPlayerItem` propriedades `subtitlesOptions`.

Para expor legendas:

1. Registre o cliente como um ouvinte para a notificação `PTMediaPlayerMediaSelectionOptionsAvailableNotification`.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   Quando seu cliente recebe essa notificação, as legendas estão prontas em `PTMediaPlayerItem`.
1. Implemente o método `onMediaPlayerItemMediaSelectionOptionsAvailable` semelhante ao exemplo a seguir:

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   Para obter informações sobre faixas de áudio alternativas, consulte [Áudio alternativo](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md).