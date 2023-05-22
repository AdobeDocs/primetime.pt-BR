---
description: Por padrão, ao iniciar a reprodução, a mídia de VOD começa em 0 e a mídia ativa começa no ponto de vida do cliente (DefaultMediaPlayer.LIVE_POINT).
title: Inserir um fluxo em um horário específico
exl-id: b97dbabf-e2ab-4669-a9f3-9129af938a40
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Inserir um fluxo em um horário específico{#enter-a-stream-at-a-specific-time}

Por padrão, ao iniciar a reprodução, a mídia de VOD começa em 0 e a mídia ativa começa no ponto de vida do cliente (DefaultMediaPlayer.LIVE_POINT).

Passar uma posição para `MediaPlayer.prepareToPlay`.

O TVSDK considera que essa posição é o ponto de partida para o ativo. Nenhuma operação de busca é necessária. Se a posição não estiver dentro do intervalo pesquisável, o usará a posição padrão.

Por exemplo:

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
