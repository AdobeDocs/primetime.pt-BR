---
description: Para usar as capas personalizadas, você deve gravar a personalização semelhante ao default-video-controls.css e consultar essa nova personalização no reprodutor.
title: Capas personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# Capas personalizadas{#custom-skins}

Para usar as capas personalizadas, você deve gravar a personalização semelhante ao default-video-controls.css e consultar essa nova personalização no reprodutor.

Por exemplo, você pode usar uma das seguintes opções:

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

Você pode fazer os seguintes tipos de alterações:

* Cor do primeiro plano dos botões e do texto

   Todos os controles que têm um primeiro plano estão usando a classe `vid-skin-fgcolor`. Para alterar o primeiro plano de todos os controles, percorra todos os elementos com a classe `vid-skin-fgcolor` e especifique a cor desejada.
* Cor de fundo dos botões e do texto

   Todos os controles que têm um primeiro plano estão usando a classe `vid-skin-bgcolor`. Para alterar o primeiro plano de todos os controles, percorra todos os elementos com a classe `vid-skin-bgcolor` e especifique a cor desejada.
* Forma do indicador de reprodução

   O indicador de reprodução pode ser quadrado ou redondo. Para alterar o indicador de reprodução, adicione a classe `square` ou `round` ao elemento `playhead`.
* Estilo dos giradores de buffering

   O reprodutor de referência fornece os seguintes estilos de rotação que podem ser exibidos como conteúdo de buffer do reprodutor:

   * Texto de sobreposição ( `overlay-text`)
   * Ponteiro retangular ( `spinner`)
   * Sinal ( `signal`)
   * Barras verticais ( `vertical`)

      >[!TIP]
      >
      >Para usar qualquer um dos giradores de buffering, você deve adicionar a classe no elemento de sobreposição de buffering. Por exemplo, para usar `overlay-text`, adicione as seguintes linhas no arquivo `BufferOverlay.js`:
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```

