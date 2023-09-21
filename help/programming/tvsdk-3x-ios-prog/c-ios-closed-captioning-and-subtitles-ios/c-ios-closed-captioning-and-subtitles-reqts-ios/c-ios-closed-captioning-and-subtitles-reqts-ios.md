---
description: Legendas ocultas e legendas têm diferenças únicas, e você as ativa de maneiras diferentes.
title: Requisitos para legendas e legendas ocultas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Requisitos para legendas e legendas ocultas {#requirements-for-subtitles-and-closed-captions}

Legendas ocultas e legendas têm diferenças únicas, e você as ativa de maneiras diferentes.

Os fluxos de legendas são executados em paralelo ao conteúdo principal. Legendas ocultas são parte dos pacotes de dados dos fluxos de vídeo MPEG-2.

Você deve estar ciente dos seguintes requisitos para legendas ocultas e legendas:

* **Legendas ocultas**

   * As legendas ocultas normalmente estão no mesmo idioma do áudio e também representam sons de fundo como texto.
   * Legendas ocultas são parte dos pacotes de dados dos fluxos de vídeo MPEG-2 no fluxo de transmissão de vídeo.
   * As legendas ocultas são compatíveis na medida em que forem fornecidas pela estrutura da AV Foundation.

* **Legendas**

   * As legendas normalmente estão em um idioma diferente e não incluem sons de fundo.
   * As legendas estão em fluxos que são executados em paralelo com o conteúdo principal.

     A variável `PTMediaPlayer` reproduz o conteúdo principal e os anúncios, onde o conteúdo principal pode ser ao vivo/linear ou VOD, e os anúncios podem ser antes da exibição, durante a exibição ou após a exibição.

  Estes são alguns requisitos adicionais para legendas no iOS:

   * Para carimbos de data e hora, a variável `X-TIMESTAMP-MAP` que é especificado na seção de cabeçalho do `WebVTT` arquivo, deve corresponder ao carimbo de data e hora do vídeo.

   * Para o sistema, você deve usar o iOS 6.1 ou posterior.

>[!IMPORTANT]
>
>Os requisitos de legendagem não se aplicam às legendas ocultas.
