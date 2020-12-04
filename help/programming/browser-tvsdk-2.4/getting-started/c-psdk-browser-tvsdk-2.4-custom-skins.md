---
description: Para usar as capas personalizadas, você deve gravar a personalização de forma semelhante ao default-video-control.css e consultar essa nova personalização no player.
seo-description: Para usar as capas personalizadas, você deve gravar a personalização de forma semelhante ao default-video-control.css e consultar essa nova personalização no player.
seo-title: Capas personalizadas
title: Capas personalizadas
uuid: bc71926e-0dec-4628-8248-911224a7a6c2
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Capas personalizadas{#custom-skins}

Para usar as capas personalizadas, você deve gravar a personalização de forma semelhante ao default-video-control.css e consultar essa nova personalização no player.

Por exemplo, você pode usar uma das seguintes opções:

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

Você pode fazer os seguintes tipos de alterações:

* Cor do primeiro plano dos botões e do texto

   Todos os controles que têm um primeiro plano estão usando a classe `vid-skin-fgcolor`. Para alterar o primeiro plano de todos os controles, repita todos os elementos com a classe `vid-skin-fgcolor` e especifique a cor desejada.
* Cor de fundo dos botões e do texto

   Todos os controles que têm um primeiro plano estão usando a classe `vid-skin-bgcolor`. Para alterar o primeiro plano de todos os controles, repita todos os elementos com a classe `vid-skin-bgcolor` e especifique a cor desejada.
* Forma da cabeça de brincar

   A cabeça de jogo pode ser quadrada ou redonda. Para alterar o indicador de reprodução, adicione a classe `square` ou `round` ao elemento `playhead`.
* Estilo dos pontilhados em buffer

   O player de referência fornece os seguintes estilos de pontilhados que podem ser exibidos como conteúdo de buffers do player:

   * Texto sobreposto ( `overlay-text`)
   * Girador retangular ( `spinner`)
   * Sinal ( `signal`)
   * Barras verticais ( `vertical`)

      >[!TIP]
      >
      >Para usar qualquer um dos spinners de buffering, é necessário adicionar a classe no elemento de buffering-overlay. Por exemplo, para usar `overlay-text`, adicione as seguintes linhas no arquivo `BufferOverlay.js`:
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```

