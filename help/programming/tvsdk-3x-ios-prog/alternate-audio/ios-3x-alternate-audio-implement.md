---
description: O áudio de ligação tardia usa o PTMediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
title: Acessar faixas de áudio alternativas
exl-id: c95e2bae-fcf3-4ae2-be11-fb3191b380f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Acessar faixas de áudio alternativas {#access-alternate-audio-tracks}

O áudio de ligação tardia usa o PTMediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde o MediaPlayer estar pelo menos no estado `PTMediaPlayerStatusReady` status.
1. Analise este evento:

   notificação `PTMediaPlayerItemMediaSelectionOptionsAvailable`: a lista inicial de faixas de áudio está disponível.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. Obter as faixas de áudio disponíveis do `PTMediaPlayerItem` instância.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. (Opcional) Apresente as trilhas disponíveis ao usuário.
1. Definir a faixa de áudio selecionada no `PTMediaPlayerItem` instância.
