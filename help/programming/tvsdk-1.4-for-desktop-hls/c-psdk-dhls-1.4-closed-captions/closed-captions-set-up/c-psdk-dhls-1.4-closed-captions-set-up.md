---
description: As legendas ocultas exibem a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou o visualizador está com problemas de audição.
title: Trabalhar com legendas ocultas
exl-id: 7550ef78-e87f-4cbc-91d6-9aab39e613d7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Trabalhar com legendas ocultas{#work-with-closed-captions}

As legendas ocultas exibem a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou o visualizador está com problemas de audição.

As legendas ocultas normalmente estão no mesmo idioma do áudio e também exibem sons de fundo como texto, mas as legendas normalmente estão em um idioma diferente e não incluem sons de fundo.

O TVSDK é compatível com a renderização destes formatos:

* Legendas ocultas 608 e 708, quando entregues como parte do fluxo de transporte de vídeo sobre HLS como pacotes de dados em fluxos de vídeo MPEG-2.
* Arquivos de legenda WebVTT, que são referenciados dos arquivos de manifesto M3U8 conforme definido nas especificações do HLS. Elas são disponibilizadas automaticamente como faixas de legendas ocultas no reprodutor do Primetime.

Você pode:

* Selecione uma faixa de legenda disponível para ser a faixa atual e ouça os eventos que indicam faixas adicionais disponíveis.
* Ativar ou desativar as legendas ocultas (visíveis ou não visíveis) usando o `MediaPlayer` interface.
* Selecione opções de estilo que determinam como as legendas ocultas são renderizadas pelo mecanismo de vídeo subjacente. Use o `MediaPlayerItem` para selecionar formatos, como fonte ou cor da fonte.
