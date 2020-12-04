---
description: A legendagem fechada exibe a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou quando o visualizador está com dificuldade de audição.
seo-description: A legendagem fechada exibe a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou quando o visualizador está com dificuldade de audição.
seo-title: Trabalhar com legendas ocultas
title: Trabalhar com legendas ocultas
uuid: 881266aa-3c32-4035-9547-0f363949f77b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# Trabalhar com legendas ocultas{#work-with-closed-captions}

A legendagem fechada exibe a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou quando o visualizador está com dificuldade de audição.

As legendas ocultas normalmente estão no mesmo idioma do áudio e também exibem os sons de fundo como texto, mas as legendas normalmente estão em um idioma diferente e não incluem os sons de fundo.

O TVSDK suporta a renderização destes formatos:

* Legenda 608 e 708, quando fornecida como parte do fluxo de transporte de vídeo por HLS como pacotes de dados em streams de vídeo MPEG-2.
* Arquivos de legenda WebVTT, que são referenciados dos arquivos de manifesto M3U8, conforme definido nas especificações HLS. Eles estão automaticamente disponíveis como faixas de legenda no player do Primetime.

Você pode:

* Selecione uma faixa de legenda disponível para ser a faixa atual e escute eventos que indicam outras faixas disponíveis.
* Ative ou desative as legendas ocultas (visíveis ou não visíveis) usando a interface `MediaPlayer`.
* Selecione opções de estilização que ditam como as legendas fechadas são renderizadas pelo mecanismo de vídeo subjacente. Use a interface `MediaPlayerItem` para selecionar formatos, como a cor da fonte ou da fonte.

