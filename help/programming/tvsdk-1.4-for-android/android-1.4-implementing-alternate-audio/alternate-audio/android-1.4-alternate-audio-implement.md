---
description: O áudio de ligação tardia utiliza o MediaPlayer para reproduzir um vídeo especificado numa lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
seo-description: O áudio de ligação tardia utiliza o MediaPlayer para reproduzir um vídeo especificado numa lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
seo-title: Acessar faixas de áudio alternativas
title: Acessar faixas de áudio alternativas
uuid: c7060022-29ec-43c1-811b-41cca5f5356c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Acessar faixas de áudio alternativas{#access-alternate-audio-tracks}

O áudio de ligação tardia utiliza o MediaPlayer para reproduzir um vídeo especificado numa lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde o MediaPlayer estar no estado PREPARADO.
1. Analise este evento:

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: A lista inicial de faixas de áudio está disponível.

1. Obtenha as faixas de áudio disponíveis da `MediaPlayerItem` instância.

   `mediaPlayerItem.getAudioTracks()` 1. (Opcional) Apresente as faixas disponíveis para o usuário.
1. Defina a faixa de áudio selecionada na `MediaPlayerItem` instância.

   `mediaPlayerItem.selectAudioTrack(audioTrack)`