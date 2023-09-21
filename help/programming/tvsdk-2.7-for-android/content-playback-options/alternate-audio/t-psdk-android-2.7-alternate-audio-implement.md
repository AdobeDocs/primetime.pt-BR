---
description: O áudio alternativo usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
title: Acessar faixas de áudio alternativas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Acessar faixas de áudio alternativas {#access-alternate-audio-tracks}

O áudio alternativo usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde a `MediaPlayer` estar pelo menos no estado `MediaPlayerStatus.PREPARED` status.
1. Ouça o `MediaPlayerEvent.STATUS_CHANGED` evento com status `MediaPlayerStatus.PREPARED`.

   Esta etapa significa que a lista inicial de faixas de áudio está disponível.

1. Obter as faixas de áudio disponíveis do `MediaPlayerItem` instância.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Opcional) Apresente as trilhas disponíveis ao usuário.
1. Definir a faixa de áudio selecionada no `MediaPlayerItem` instância.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
