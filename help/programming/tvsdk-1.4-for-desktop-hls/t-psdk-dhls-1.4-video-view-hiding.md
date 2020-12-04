---
description: Depois que uma visualização MediaPlayer é usada para reproduzir vídeo, você pode ocultá-la e exibi-la novamente usando um método TVSDK ou manualmente.
seo-description: Depois que uma visualização MediaPlayer é usada para reproduzir vídeo, você pode ocultá-la e exibi-la novamente usando um método TVSDK ou manualmente.
seo-title: Ocultar uma visualização de vídeo
title: Ocultar uma visualização de vídeo
uuid: 7cc02bf4-41ee-4af0-98ba-df070b50b88d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---


# Ocultar uma visualização de vídeo{#hide-a-video-view}

Depois que uma visualização MediaPlayer é usada para reproduzir vídeo, você pode ocultá-la e exibi-la novamente usando um método TVSDK ou manualmente.

Você deve pausar um vídeo antes de apagá-lo ou movê-lo da tela.
* Opção 1: Limpe o quadro de vídeo com `MediaPlayer.clearVideo` &#x200B; e substitua o quadro mais tarde.
   * Pause o vídeo que deseja ocultar.
   * Remova o quadro de vídeo exibido chamando `MediaPlayer.clearVideo`.
   * Para redefinir `MediaPlayer` para que possa ser reproduzido novamente, chame `replaceCurrentResource` ou `replaceCurrentItem`.
* Opção 2: Mova a visualização `MediaPlayer` para fora da tela e mova-a de volta mais tarde sem precisar substituí-la.
   * Pause o vídeo que deseja ocultar.
   * Mova a visualização para fora do palco. Por exemplo:

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * Para exibir o vídeo novamente, mova a visualização de volta ao palco.
