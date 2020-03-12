---
description: O áudio de ligação tardia utiliza o MediaPlayer para reproduzir um vídeo especificado numa lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
seo-description: O áudio de ligação tardia utiliza o MediaPlayer para reproduzir um vídeo especificado numa lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
seo-title: Acessar faixas de áudio alternativas
title: Acessar faixas de áudio alternativas
uuid: 136b4f1b-e56f-4a8a-a961-05193434558c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Acessar faixas de áudio alternativas{#access-alternate-audio-tracks}

O áudio de ligação tardia utiliza o MediaPlayer para reproduzir um vídeo especificado numa lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde até `MediaPlayer` o estado PREPARADO.
1. Analise estes eventos:

   * `MediaPlayerItemEvent.ITEM_CREATED`: A lista inicial de faixas de áudio está disponível.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`: Faixas de áudio alteradas durante a reprodução

1. Obtenha as faixas de áudio disponíveis da `MediaPlayerItem` instância.
1. (Opcional) Apresente as faixas disponíveis para o usuário.
1. Defina a faixa de áudio selecionada na `MediaPlayerItem` instância.
