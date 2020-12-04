---
description: Por padrão, ao iniciar a reprodução, start de mídia VOD em 0 e start de mídia ao vivo no ponto ativo do cliente (DefaultMediaPlayer.LIVE_POINT).
seo-description: Por padrão, ao iniciar a reprodução, start de mídia VOD em 0 e start de mídia ao vivo no ponto ativo do cliente (DefaultMediaPlayer.LIVE_POINT).
seo-title: Insira um fluxo em um horário específico
title: Insira um fluxo em um horário específico
uuid: f58d908a-77b9-465f-b3a9-8fe63a249d39
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 1%

---


# Insira um fluxo em um horário específico{#enter-a-stream-at-a-specific-time}

Por padrão, ao iniciar a reprodução, start de mídia VOD em 0 e start de mídia ao vivo no ponto ativo do cliente (DefaultMediaPlayer.LIVE_POINT).

Passe uma posição para `MediaPlayer.prepareToPlay`.

O TVSDK considera a posição fornecida como o ponto de partida para o ativo. Nenhuma operação de busca é necessária. Se a posição não estiver dentro do intervalo pesquisável, use a posição padrão.

Por exemplo:

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
