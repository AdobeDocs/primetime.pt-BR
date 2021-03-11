---
description: É possível controlar a posição e o tamanho da exibição de vídeo usando o objeto MediaPlayerView .
title: Controlar a posição e o tamanho da exibição de vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# Controlar a posição e o tamanho da visualização de vídeo{#control-the-position-and-size-of-the-video-view}

É possível controlar a posição e o tamanho da exibição de vídeo usando o objeto MediaPlayerView .

Por padrão, o TVSDK tenta manter a proporção da exibição de vídeo sempre que o tamanho ou a posição do vídeo é alterado (devido a uma alteração feita pelo aplicativo, por um switch de perfil, por um switch de conteúdo etc.).

Você pode substituir o comportamento da taxa de proporção padrão especificando uma *política de escala* diferente. Especifique a política de escala usando a propriedade `MediaPlayerView` do objeto `scalePolicy`. A política de escala padrão de `MediaPlayerView` é definida com uma instância da classe `MaintainAspectRatioScalePolicy`. Para redefinir a política de escala, substitua a instância padrão de `MaintainAspectRatioScalePolicy` em `MediaPlayerView.scalePolicy` por sua própria política. (Não é possível definir a propriedade `scalePolicy` para um valor nulo.)

1. Implemente a interface `MediaPlayerViewScalePolicy` para criar sua própria política de escala.

   O `MediaPlayerViewScalePolicy` tem um método:

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >O TVSDK usa um objeto `StageVideo` para exibir o vídeo e, como os objetos `StageVideo` não estão na lista de exibição, o parâmetro `viewPort` contém as coordenadas absolutas do vídeo.
   >
   >
   >Por exemplo:
   >
   >
   ```
   >public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
   >       /** 
   >         * Default constructor. 
   >         */ 
   >       public function CustomScalePolicy() { 
   >       } 
   > 
   >    
      public function adjust(viewPort:Rectangle,  
   >                                                     videoWidth:Number,  
   >                                                     videoHeight:Number):Rectangle { 
   >               return customAdjustment(); 
   >       } 
   > 
   >    
      public function customAdjustment():Rectangle { 
   >               /* Your custom adjustment here */ 
   >               [...] 
   >       } 
   >}
   >```

1. Atribua sua implementação à propriedade `MediaPlayerView` .

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. Adicione sua visualização à propriedade `view` do Media Player.

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**Por exemplo: Dimensione o vídeo para preencher a visualização de vídeo inteira, sem manter a proporção:**

```
package com.adobe.mediacore.samples.utils { 
    import com.adobe.mediacore.view.MediaPlayerViewScalePolicy; 
    import flash.geom.Rectangle; 
 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
 
        /** 
        * Default constructor. 
        */ 
        public function CustomScalePolicy() { 
        } 
 
        public function adjust(viewPort:Rectangle, 
                               videoWidth:Number,  
                               videoHeight:Number):Rectangle { 
            return viewPort; 
        } 
    } 
} 
 
var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
view.scalePolicy = new CustomScalePolicy(); 
addChild(view); 
mediaPlayer.view = view;
```

