---
description: O áudio de ligação tardia usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.
title: Acessar faixas de áudio alternativas
exl-id: 08158b3b-1ed2-4f86-a710-2b128bb28ed0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Acessar faixas de áudio alternativas{#access-alternate-audio-tracks}

O áudio de ligação tardia usa o MediaPlayer para reproduzir um vídeo especificado em uma lista de reprodução HLS M3U8 e que pode conter vários fluxos de áudio alternativos.

1. Aguarde a `MediaPlayer` estar pelo menos no status PREPARADO.
1. Ouça estes eventos:

   * `MediaPlayerItemEvent.ITEM_CREATED`: a lista inicial de faixas de áudio está disponível.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`: faixas de áudio alteradas durante a reprodução

1. Obter as faixas de áudio disponíveis do `MediaPlayerItem` instância.
1. (Opcional) Apresente as trilhas disponíveis ao usuário.
1. Definir a faixa de áudio selecionada no `MediaPlayerItem` instância.
