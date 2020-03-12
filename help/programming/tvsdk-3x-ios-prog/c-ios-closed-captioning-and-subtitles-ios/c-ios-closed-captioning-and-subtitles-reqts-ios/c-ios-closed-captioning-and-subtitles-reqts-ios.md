---
description: As legendas e legendas ocultas têm algumas diferenças exclusivas e você as ativa de diferentes maneiras.
seo-description: As legendas e legendas ocultas têm algumas diferenças exclusivas e você as ativa de diferentes maneiras.
seo-title: Requisitos para legendas e legendas ocultas
title: Requisitos para legendas e legendas ocultas
uuid: 18ed6ac1-4b25-4590-8c61-3ffb0464d093
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Requisitos para legendas e legendas ocultas {#requirements-for-subtitles-and-closed-captions}

As legendas e legendas ocultas têm algumas diferenças exclusivas e você as ativa de diferentes maneiras.

Os fluxos de legendas são executados em paralelo ao conteúdo principal. As legendas ocultas fazem parte dos pacotes de dados dos fluxos de vídeo MPEG-2.

Você deve estar ciente dos seguintes requisitos para legendas e legendas fechadas:

* **Legendas ocultas**

   * As legendas ocultas normalmente estão no mesmo idioma do áudio e também representam sons de fundo como texto.
   * As legendas ocultas fazem parte dos pacotes de dados dos fluxos de vídeo MPEG-2 no fluxo de transmissão de vídeo.
   * As legendas ocultas são suportadas na medida fornecida pela estrutura da Fundação AV.

* **Legendas**

   * As legendas normalmente estão em um idioma diferente e não incluem sons de fundo.
   * As legendas estão em fluxos que são executados em paralelo ao conteúdo principal.

      O `PTMediaPlayer` reproduz o conteúdo e os anúncios principais, onde o conteúdo principal pode ser live/linear ou VOD, e os anúncios podem ser pre-roll, mid-roll ou post-roll.
   Estes são alguns requisitos adicionais para legendas no iOS:

   * Para carimbos de data e hora, o `X-TIMESTAMP-MAP` valor, que é especificado na seção de cabeçalho do `WebVTT` arquivo, deve corresponder ao carimbo de data e hora do vídeo.

   * Para o sistema, você deve usar o iOS 6.1 ou posterior.


>[!IMPORTANT]
>
>Os requisitos para legendas não se aplicam a legendas fechadas.