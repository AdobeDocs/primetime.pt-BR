---
description: As legendas ocultas exibem a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou o visualizador está com problemas de audição.
title: Trabalhar com legendas ocultas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Visão geral {#work-with-closed-captions-overview}

As legendas ocultas exibem a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou o visualizador está com problemas de audição.

As legendas ocultas normalmente estão no mesmo idioma do áudio e também exibem sons de fundo como texto, mas as legendas normalmente estão em um idioma diferente e não incluem sons de fundo.

O TVSDK é compatível com a renderização destes formatos:

* Legendas ocultas 608 e 708, quando entregues como parte do fluxo de transporte de vídeo sobre HLS como pacotes de dados em fluxos de vídeo MPEG-2.
* Arquivos de legenda WebVTT, que são referenciados dos arquivos de manifesto M3U8 conforme definido nas especificações do HLS.

  Esses arquivos são disponibilizados automaticamente como faixas de legendas ocultas no reprodutor do Primetime.

Você pode fazer o seguinte:

* Selecione uma faixa de legenda disponível para ser a faixa atual e ouça os eventos que indicam faixas adicionais disponíveis.
* Ativar (visível) ou desativar (não visível) as legendas ocultas usando o `MediaPlayer` interface.
* Selecione opções de estilo que determinam como as legendas ocultas são renderizadas pelo mecanismo de vídeo subjacente.

  Use o `MediaPlayerItem` para selecionar formatos, como fonte ou cor da fonte.
