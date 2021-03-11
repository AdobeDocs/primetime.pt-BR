---
description: O áudio de ligação tardia usa o MediaPlayer para reproduzir um vídeo especificado numa lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
title: Acessar trilhas de áudio alternativas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Acessar trilhas de áudio alternativas{#access-alternate-audio-tracks}

O áudio de ligação tardia usa o MediaPlayer para reproduzir um vídeo especificado numa lista de reprodução de HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde até que `MediaPlayer` esteja pelo menos no status PREPARED.
1. Analise estes eventos:

   * `MediaPlayerItemEvent.ITEM_CREATED`: A lista inicial de faixas de áudio está disponível.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`: Trilhas de áudio alteradas durante a reprodução

1. Obtenha as faixas de áudio disponíveis da instância `MediaPlayerItem`.
1. (Opcional) Apresente as faixas disponíveis para o usuário.
1. Defina a faixa de áudio selecionada na instância `MediaPlayerItem`.
