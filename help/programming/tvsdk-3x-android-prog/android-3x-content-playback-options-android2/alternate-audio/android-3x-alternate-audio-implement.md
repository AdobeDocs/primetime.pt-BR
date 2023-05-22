---
description: O áudio alternativo usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
title: Acessar faixas de áudio alternativas
exl-id: 88fa8f42-59d7-4a57-90c6-4c23b2ea7e00
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Acessar faixas de áudio alternativas{#access-alternate-audio-tracks}

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
