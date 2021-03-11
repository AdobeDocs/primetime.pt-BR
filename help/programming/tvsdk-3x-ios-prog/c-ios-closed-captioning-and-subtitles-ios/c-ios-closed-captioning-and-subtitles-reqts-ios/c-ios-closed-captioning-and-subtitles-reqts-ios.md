---
description: As legendas e legendas ocultas têm algumas diferenças exclusivas, e você as habilita de diferentes maneiras.
title: Requisitos para legendas e legendas ocultas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Requisitos para legendas e legendas ocultas {#requirements-for-subtitles-and-closed-captions}

As legendas e legendas ocultas têm algumas diferenças exclusivas, e você as habilita de diferentes maneiras.

Fluxos de subtítulos são executados em paralelo com o conteúdo principal. As legendas ocultas fazem parte dos pacotes de dados dos fluxos de vídeo MPEG-2.

Você deve estar ciente dos seguintes requisitos para legendas e legendas ocultas:

* **Legendas ocultas**

   * As legendas ocultas normalmente estão no mesmo idioma do áudio e também representam sons de fundo como texto.
   * As legendas ocultas são parte dos pacotes de dados dos fluxos de vídeo MPEG-2 no fluxo de transmissão de vídeo.
   * As legendas ocultas são compatíveis na medida em que forem fornecidas pela estrutura da AV Foundation.

* **Legendas**

   * As legendas normalmente estão em um idioma diferente e não incluem sons de fundo.
   * As legendas estão em fluxos que são executados em paralelo com o conteúdo principal.

      O `PTMediaPlayer` reproduz o conteúdo e os anúncios principais, onde o conteúdo principal pode ser ao vivo/linear ou VOD, e os anúncios podem ser precedentes, intermediários ou posteriores.
   Estes são alguns requisitos adicionais para legendas no iOS:

   * Para carimbos de data e hora, o valor `X-TIMESTAMP-MAP`, que é especificado na seção de cabeçalho do arquivo `WebVTT`, deve corresponder ao carimbo de data e hora do vídeo.

   * Para o sistema, você deve usar o iOS 6.1 ou posterior.


>[!IMPORTANT]
>
>Os requisitos para legendas não se aplicam a legendas ocultas.