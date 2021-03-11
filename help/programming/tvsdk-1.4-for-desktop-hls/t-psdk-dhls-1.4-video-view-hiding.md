---
description: Depois que uma exibição do MediaPlayer é usada para reproduzir o vídeo, é possível ocultá-la e exibi-la novamente usando um método TVSDK ou manualmente.
title: Ocultar uma visualização de vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 1%

---


# Ocultar uma visualização de vídeo{#hide-a-video-view}

Depois que uma exibição do MediaPlayer é usada para reproduzir o vídeo, é possível ocultá-la e exibi-la novamente usando um método TVSDK ou manualmente.

Você deve pausar um vídeo antes de limpá-lo ou movê-lo da tela.
* Opção 1: Limpe o quadro de vídeo com `MediaPlayer.clearVideo` &#x200B; e substitua o quadro posteriormente.
   * Pause o vídeo que deseja ocultar.
   * Remova o quadro de vídeo exibido chamando `MediaPlayer.clearVideo`.
   * Para redefinir o `MediaPlayer` para que ele possa ser reproduzido novamente, chame `replaceCurrentResource` ou `replaceCurrentItem`.
* Opção 2: Mova a visualização `MediaPlayer` para fora da tela e mova-a de volta mais tarde sem precisar substituí-la.
   * Pause o vídeo que deseja ocultar.
   * Mova a exibição para fora do palco. Por exemplo:

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * Para exibir o vídeo novamente, mova a visualização de volta para o palco.
