---
description: Para usar as capas personalizadas, você deve gravar a personalização de forma semelhante a default-video-controls.css e consultar essa nova personalização no reprodutor.
title: Capas personalizadas
exl-id: 4d627545-942d-4883-a010-afddcffb8dd5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Capas personalizadas{#custom-skins}

Para usar as capas personalizadas, você deve gravar a personalização de forma semelhante a default-video-controls.css e consultar essa nova personalização no reprodutor.

Por exemplo, você pode usar uma das seguintes opções:

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

Você pode fazer os seguintes tipos de alterações:

* Cor de primeiro plano dos botões e texto

   Todos os controles que têm um primeiro plano estão usando o `vid-skin-fgcolor` classe. Para alterar o primeiro plano de todos os controles, percorra todos os elementos com o `vid-skin-fgcolor` e especifique a cor desejada.
* Cor de fundo dos botões e texto

   Todos os controles com um primeiro plano estão usando o `vid-skin-bgcolor` classe. Para alterar o primeiro plano de todos os controles, repita todos os elementos com `vid-skin-bgcolor` e especifique a cor desejada.
* Forma da cabeça de jogo

   A cabeça de jogo pode ser quadrada ou redonda. Para alterar o indicador de reprodução, adicione `square` ou `round` classe para `playhead` elemento.
* Estilo dos spinners de buffering

   O reprodutor de referência fornece os seguintes estilos de spinners que podem ser exibidos como conteúdo de buffers do reprodutor:

   * Texto de sobreposição ( `overlay-text`)
   * Indicador de rotação retangular ( `spinner`)
   * Sinal ( `signal`)
   * Barras verticais ( `vertical`)

      >[!TIP]
      >
      >Para usar qualquer um dos spinners de buffering, você deve adicionar a classe no elemento buffering-overlay. Por exemplo, para usar `overlay-text`, adicione as seguintes linhas no `BufferOverlay.js` arquivo:
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```
