---
description: O TVSDK notifica o cliente do player sobre a disponibilidade de availableMediaCharacteristicsWithMediaSelectionOptions do AVAsset interno usando a notificação PTMediaPlayerMediaSelectionOptionsAvailableNotification.
title: Expor legendas
exl-id: 42f15536-39ea-4d83-b501-b05086a0056b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Expor legendas {#expose-subtitles}

O TVSDK notifica o cliente do player sobre a disponibilidade de availableMediaCharacteristicsWithMediaSelectionOptions do AVAsset interno usando a notificação PTMediaPlayerMediaSelectionOptionsAvailableNotification.

É possível acessar as legendas disponíveis através da `PTMediaPlayerItem` da propriedade `subtitlesOptions`.

Para expor as legendas:

1. Registre o cliente como um listener para o `PTMediaPlayerMediaSelectionOptionsAvailableNotification` notificação.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   Quando seu cliente receber essa notificação, as legendas estarão prontas no `PTMediaPlayerItem`.
1. Implementar o `onMediaPlayerItemMediaSelectionOptionsAvailable` método semelhante ao seguinte exemplo:

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   Para obter informações sobre faixas de áudio alternativas, consulte  [Áudio Alternativo](../../alternate-audio/ios-3x-alternate-audio.md).
