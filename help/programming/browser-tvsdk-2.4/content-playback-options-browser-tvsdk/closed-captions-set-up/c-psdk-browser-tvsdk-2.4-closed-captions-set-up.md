---
description: As legendas ocultas exibem a parte de áudio de um vídeo como texto na tela quando o som é inaudível ou o visualizador não consegue ouvir.
title: Trabalhar com legendas ocultas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Trabalhar com legendas ocultas{#work-with-closed-captions}

As legendas ocultas exibem a parte de áudio de um vídeo como texto na tela quando o som é inaudível ou o visualizador não consegue ouvir.

As legendas ocultas normalmente estão no mesmo idioma do áudio e também exibem os sons de fundo como texto, mas as legendas normalmente estão em um idioma diferente e não incluem sons de fundo.

O TVSDK do navegador suporta a renderização desses formatos:

* Legendas ocultas 608 e 708, quando fornecidas como parte do fluxo de transporte de vídeo por HLS como pacotes de dados em fluxos de vídeo MPEG-2.
* Arquivos de legenda WebVTT, que são referenciados dos arquivos de manifesto M3U8, conforme definido nas especificações HLS. Eles ficam disponíveis automaticamente como faixas de legenda fechada no player do Primetime.

É possível:

* Selecione um rastreamento de legenda disponível para ser o rastreamento atual e acompanhar eventos que indicam faixas adicionais disponíveis.
* Ative ou desative as legendas ocultas (visível ou não visível) usando a interface `MediaPlayer`.
* Selecione as opções de estilo que determinam como as legendas ocultas são renderizadas pelo mecanismo de vídeo subjacente. Use a interface `MediaPlayerItem` para selecionar formatos, como a fonte ou a cor da fonte.

