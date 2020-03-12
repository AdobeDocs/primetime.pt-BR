---
description: Para usar as capas personalizadas, você deve gravar a personalização de forma semelhante ao default-video-control.css e consultar essa nova personalização no player.
seo-description: Para usar as capas personalizadas, você deve gravar a personalização de forma semelhante ao default-video-control.css e consultar essa nova personalização no player.
seo-title: Capas personalizadas
title: Capas personalizadas
uuid: bc71926e-0dec-4628-8248-911224a7a6c2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Capas personalizadas{#custom-skins}

Para usar as capas personalizadas, você deve gravar a personalização de forma semelhante ao default-video-control.css e consultar essa nova personalização no player.

Por exemplo, você pode usar uma das seguintes opções:

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

Você pode fazer os seguintes tipos de alterações:

* Cor do primeiro plano dos botões e do texto

   Todos os controles que têm um primeiro plano estão usando a `vid-skin-fgcolor` classe. Para alterar o primeiro plano de todos os controles, repita todos os elementos com a `vid-skin-fgcolor` classe e especifique a cor desejada.
* Cor de fundo dos botões e do texto

   Todos os controles que têm um primeiro plano estão usando a `vid-skin-bgcolor` classe. Para alterar o primeiro plano de todos os controles, repita todos os elementos com a `vid-skin-bgcolor` classe e especifique a cor desejada.
* Forma da cabeça de brincar

   A cabeça de jogo pode ser quadrada ou redonda. Para alterar o indicador de reprodução, adicione `square` ou `round` classe ao `playhead` elemento.
* Estilo dos pontilhados em buffer

   O player de referência fornece os seguintes estilos de pontilhados que podem ser exibidos como conteúdo de buffers do player:

   * Texto sobreposto ( `overlay-text`)
   * Girador Retangular ( `spinner`)
   * Sinal ( `signal`)
   * Barras verticais ( `vertical`)

      >[!TIP]
      >
      >Para usar qualquer um dos spinners de buffering, é necessário adicionar a classe no elemento de buffering-overlay. Por exemplo, para usar `overlay-text`, adicione as seguintes linhas no `BufferOverlay.js` arquivo:       >
      >
      >
      ```js      >
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```      >
      >



