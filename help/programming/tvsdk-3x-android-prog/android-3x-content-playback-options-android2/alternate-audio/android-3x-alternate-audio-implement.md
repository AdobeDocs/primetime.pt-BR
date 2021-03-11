---
description: O áudio alternativo usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
title: Acessar trilhas de áudio alternativas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Acessar trilhas de áudio alternativas{#access-alternate-audio-tracks}

O áudio alternativo usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde até que `MediaPlayer` esteja pelo menos no status `MediaPlayerStatus.PREPARED`.
1. Analise o evento `MediaPlayerEvent.STATUS_CHANGED` com o status `MediaPlayerStatus.PREPARED`.

   Esta etapa significa que a lista inicial de trilhas de áudio está disponível.

1. Obtenha as faixas de áudio disponíveis da instância `MediaPlayerItem`.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Opcional) Apresente as faixas disponíveis para o usuário.
1. Defina a faixa de áudio selecionada na instância `MediaPlayerItem`.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
