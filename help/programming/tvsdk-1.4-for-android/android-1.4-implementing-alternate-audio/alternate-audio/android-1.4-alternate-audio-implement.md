---
description: O áudio de ligação tardia usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
title: Acessar faixas de áudio alternativas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# Acessar faixas de áudio alternativas{#access-alternate-audio-tracks}

O áudio de ligação tardia usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde o MediaPlayer estar pelo menos no estado PREPARADO.
1. Analise este evento:

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: a lista inicial de faixas de áudio está disponível.

1. Obter as faixas de áudio disponíveis do `MediaPlayerItem` instância.

   `mediaPlayerItem.getAudioTracks()` 1. (Opcional) Apresente as trilhas disponíveis ao usuário.
1. Definir a faixa de áudio selecionada no `MediaPlayerItem` instância.

   `mediaPlayerItem.selectAudioTrack(audioTrack)`
