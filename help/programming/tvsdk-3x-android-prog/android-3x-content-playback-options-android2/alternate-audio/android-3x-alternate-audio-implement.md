---
description: O áudio alternativo usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
seo-description: O áudio alternativo usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
seo-title: Acessar faixas de áudio alternativas
title: Acessar faixas de áudio alternativas
uuid: 09aa00e9-0cbf-4f5b-9652-ce514f6e2f38
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---


# Acessar faixas de áudio alternativas{#access-alternate-audio-tracks}

O áudio alternativo usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde até que `MediaPlayer` esteja pelo menos no status `MediaPlayerStatus.PREPARED`.
1. Analise o evento `MediaPlayerEvent.STATUS_CHANGED` com o status `MediaPlayerStatus.PREPARED`.

   Essa etapa significa que a lista inicial das faixas de áudio está disponível.

1. Obtenha as faixas de áudio disponíveis da instância `MediaPlayerItem`.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Opcional) Apresente as faixas disponíveis para o usuário.
1. Defina a faixa de áudio selecionada na instância `MediaPlayerItem`.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
