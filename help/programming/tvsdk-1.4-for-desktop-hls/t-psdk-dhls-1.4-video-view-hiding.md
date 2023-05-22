---
description: Depois que uma visualização do MediaPlayer for usada para reproduzir o vídeo, você poderá ocultá-lo e exibi-lo novamente usando um método TVSDK ou manualmente.
title: Ocultar uma visualização de vídeo
exl-id: 92354cd3-f0ed-4434-a7af-a3545e0e2460
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Ocultar uma visualização de vídeo{#hide-a-video-view}

Depois que uma visualização do MediaPlayer for usada para reproduzir o vídeo, você poderá ocultá-lo e exibi-lo novamente usando um método TVSDK ou manualmente.

Você deve pausar um vídeo antes de limpá-lo ou movê-lo da exibição.
* Opção 1: limpar o quadro do vídeo com `MediaPlayer.clearVideo`&#x200B; e substitua o quadro mais tarde.
   * Pausar o vídeo que você deseja ocultar.
   * Remova o quadro de vídeo exibido chamando `MediaPlayer.clearVideo`.
   * Para redefinir o `MediaPlayer` para que possa ser reproduzido novamente, chame `replaceCurrentResource` ou `replaceCurrentItem`.
* Opção 2: mover o `MediaPlayer` exibir fora da tela e movê-lo de volta mais tarde sem ter que substituí-lo.
   * Pausar o vídeo que você deseja ocultar.
   * Mova a exibição para fora do estágio. Por exemplo:

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * Para exibir o vídeo novamente, mova a exibição de volta para o palco.
