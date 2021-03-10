---
description: Por padrão, ao iniciar a reprodução, a mídia VOD é iniciada em 0 e a mídia ao vivo é iniciada no ponto ativo do cliente (DefaultMediaPlayer.LIVE_POINT).
title: Insira um fluxo em um horário específico
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

---


# Insira um fluxo em um horário específico{#enter-a-stream-at-a-specific-time}

Por padrão, ao iniciar a reprodução, a mídia VOD é iniciada em 0 e a mídia ao vivo é iniciada no ponto ativo do cliente (DefaultMediaPlayer.LIVE_POINT).

Passe uma posição para `MediaPlayer.prepareToPlay`.

O TVSDK considera a posição fornecida como o ponto de partida para o ativo. Nenhuma operação de busca é necessária. Se a posição não estiver dentro do intervalo pesquisável, o usará a posição padrão.

Por exemplo:

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
