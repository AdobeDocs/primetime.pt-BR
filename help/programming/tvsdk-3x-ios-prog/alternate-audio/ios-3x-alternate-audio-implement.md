---
description: O áudio de ligação tardia utiliza o PTMediaPlayer para reproduzir um vídeo especificado numa lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
title: Acessar trilhas de áudio alternativas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Acessar trilhas de áudio alternativas {#access-alternate-audio-tracks}

O áudio de ligação tardia utiliza o PTMediaPlayer para reproduzir um vídeo especificado numa lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde até que o MediaPlayer esteja pelo menos no status `PTMediaPlayerStatusReady`.
1. Analise este evento:

   notificação `PTMediaPlayerItemMediaSelectionOptionsAvailable`: A lista inicial de faixas de áudio está disponível.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. Obtenha as faixas de áudio disponíveis da instância `PTMediaPlayerItem`.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. (Opcional) Apresente as faixas disponíveis para o usuário.
1. Defina a faixa de áudio selecionada na instância `PTMediaPlayerItem`.
