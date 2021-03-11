---
description: O áudio de ligação tardia usa o MediaPlayer para reproduzir um vídeo especificado numa lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
title: Acessar trilhas de áudio alternativas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---


# Acessar trilhas de áudio alternativas{#access-alternate-audio-tracks}

O áudio de ligação tardia usa o MediaPlayer para reproduzir um vídeo especificado numa lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde até que o MediaPlayer esteja pelo menos no estado PREPARADO.
1. Analise este evento:

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: A lista inicial de faixas de áudio está disponível.

1. Obtenha as faixas de áudio disponíveis da instância `MediaPlayerItem`.

   `mediaPlayerItem.getAudioTracks()` 1. (Opcional) Apresente as faixas disponíveis para o usuário.
1. Defina a faixa de áudio selecionada na instância `MediaPlayerItem`.

   `mediaPlayerItem.selectAudioTrack(audioTrack)`