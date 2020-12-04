---
description: A legendagem fechada exibe a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou quando o visualizador está com dificuldade de audição.
seo-description: A legendagem fechada exibe a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou quando o visualizador está com dificuldade de audição.
seo-title: Trabalhar com legendas ocultas
title: Trabalhar com legendas ocultas
uuid: d7860de4-2881-4817-a4cc-5e7ab557a1db
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# Visão geral {#work-with-closed-captions-overview}

A legendagem fechada exibe a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou quando o visualizador está com dificuldade de audição.

As legendas ocultas normalmente estão no mesmo idioma do áudio e também exibem os sons de fundo como texto, mas as legendas normalmente estão em um idioma diferente e não incluem os sons de fundo.

O TVSDK suporta a renderização destes formatos:

* Legenda 608 e 708, quando fornecida como parte do fluxo de transporte de vídeo por HLS como pacotes de dados em streams de vídeo MPEG-2.
* Arquivos de legenda WebVTT, que são referenciados dos arquivos de manifesto M3U8, conforme definido nas especificações HLS.

   Esses arquivos estão automaticamente disponíveis como faixas de legenda no player do Primetime.

Você pode fazer o seguinte:

* Selecione uma faixa de legenda disponível para ser a faixa atual e escute eventos que indicam outras faixas disponíveis.
* Ative ou desative as legendas fechadas (visível) usando a interface `MediaPlayer`.
* Selecione opções de estilização que ditam como as legendas fechadas são renderizadas pelo mecanismo de vídeo subjacente.

   Use a interface `MediaPlayerItem` para selecionar formatos, como a cor da fonte ou da fonte.