---
description: O áudio de ligação tardia usa o PTMediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
seo-description: O áudio de ligação tardia usa o PTMediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
seo-title: Acessar faixas de áudio alternativas
title: Acessar faixas de áudio alternativas
uuid: 77e39633-bf17-4a06-a2a1-93fdaadedd17
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Acessar faixas de áudio alternativas{#access-alternate-audio-tracks}

O áudio de ligação tardia usa o PTMediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde o MediaPlayer ter pelo menos o `PTMediaPlayerStatusReady` status.
1. Analise este evento:

   notificação `PTMediaPlayerItemMediaSelectionOptionsAvailable`: A lista inicial de faixas de áudio está disponível.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. Obtenha as faixas de áudio disponíveis da `PTMediaPlayerItem` instância.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. (Opcional) Apresente as faixas disponíveis para o usuário.
1. Defina a faixa de áudio selecionada na `PTMediaPlayerItem` instância.
