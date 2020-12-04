---
description: O áudio de ligação tardia usa o PTMediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
seo-description: O áudio de ligação tardia usa o PTMediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
seo-title: Acessar faixas de áudio alternativas
title: Acessar faixas de áudio alternativas
uuid: 2915a74f-5ec3-457e-890d-5c79be39f37a
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Acessar faixas de áudio alternativas {#access-alternate-audio-tracks}

O áudio de ligação tardia usa o PTMediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde até que o MediaPlayer esteja pelo menos no status `PTMediaPlayerStatusReady`.
1. Ouça este evento:

   notificação `PTMediaPlayerItemMediaSelectionOptionsAvailable`: A lista inicial das faixas de áudio está disponível.

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
