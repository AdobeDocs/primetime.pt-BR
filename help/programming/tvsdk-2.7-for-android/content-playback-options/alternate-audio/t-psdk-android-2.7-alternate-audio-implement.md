---
description: O áudio alternativo usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
seo-description: O áudio alternativo usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
seo-title: Acessar faixas de áudio alternativas
title: Acessar faixas de áudio alternativas
uuid: 9cec3a00-1416-497d-8d16-0ee429c8b575
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Acessar faixas de áudio alternativas {#access-alternate-audio-tracks}

O áudio alternativo usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde até `MediaPlayer` que o usuário tenha pelo menos o `MediaPlayerStatus.PREPARED` status.
1. Ouça o `MediaPlayerEvent.STATUS_CHANGED` evento com status `MediaPlayerStatus.PREPARED`.

   Essa etapa significa que a lista inicial de faixas de áudio está disponível.

1. Obtenha as faixas de áudio disponíveis da `MediaPlayerItem` instância.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Opcional) Apresente as faixas disponíveis para o usuário.
1. Defina a faixa de áudio selecionada na `MediaPlayerItem` instância.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```

