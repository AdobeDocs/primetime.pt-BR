---
description: A legendagem fechada exibe a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou quando o visualizador está com dificuldade de audição.
seo-description: A legendagem fechada exibe a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou quando o visualizador está com dificuldade de audição.
seo-title: Selecionar uma faixa de legenda atual entre as faixas disponíveis
title: Selecionar uma faixa de legenda atual entre as faixas disponíveis
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Visão geral {#work-with-closed-captions}

A legendagem fechada exibe a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou quando o visualizador está com dificuldade de audição.

As legendas ocultas normalmente estão no mesmo idioma do áudio e também exibem os sons de fundo como texto, mas as legendas normalmente estão em um idioma diferente e não incluem os sons de fundo.

O TVSDK suporta a renderização destes formatos:

* Legenda 608 e 708, quando fornecida como parte do fluxo de transporte de vídeo por HLS como pacotes de dados em streams de vídeo MPEG-2.
* Arquivos de legenda WebVTT, que são referenciados dos arquivos de manifesto M3U8, conforme definido nas especificações HLS. Eles estão automaticamente disponíveis como faixas de legenda no player do Primetime.

Você pode:

* Selecione uma faixa de legenda disponível para ser a faixa atual e escute eventos que indicam outras faixas disponíveis.
* Ative ou desative as legendas ocultas (visíveis ou não visíveis) usando a interface `MediaPlayer`.
* Selecione opções de estilização que ditam como as legendas fechadas são renderizadas pelo mecanismo de vídeo subjacente. Use a interface `MediaPlayerItem` para selecionar formatos, como a cor da fonte ou da fonte.
