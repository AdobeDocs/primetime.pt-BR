---
description: É possível controlar a posição e o tamanho da visualização de vídeo usando o objeto MediaPlayerView.
seo-description: É possível controlar a posição e o tamanho da visualização de vídeo usando o objeto MediaPlayerView.
seo-title: Controlar a posição e o tamanho da visualização de vídeo
title: Controlar a posição e o tamanho da visualização de vídeo
uuid: 2231c574-03cd-45a8-ab00-4a42f8e044f0
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Controlar a posição e o tamanho da visualização de vídeo{#control-the-position-and-size-of-the-video-view}

É possível controlar a posição e o tamanho da visualização de vídeo usando o objeto MediaPlayerView.

Por padrão, o TVSDK tenta manter a proporção da visualização de vídeo sempre que o tamanho ou a posição do vídeo mudar (devido a uma alteração feita pelo aplicativo, ou por um switch de perfil, ou por um switch de conteúdo etc.).

Você pode substituir o comportamento padrão de proporção especificando uma política *de* escala diferente. Especifique a política de escala usando a propriedade do `MediaPlayerView` objeto `scalePolicy` . A política de escala padrão `MediaPlayerView`da é definida com uma instância da `MaintainAspectRatioScalePolicy` classe. Para redefinir a política de escala, substitua a instância padrão de `MaintainAspectRatioScalePolicy` on por `MediaPlayerView.scalePolicy` sua própria política. (Não é possível definir a `scalePolicy` propriedade como um valor nulo.)

1. Implemente a `MediaPlayerViewScalePolicy` interface para criar sua própria política de escala.

   O `MediaPlayerViewScalePolicy` tem um método:

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >O TVSDK usa um `StageVideo` objeto para exibir o vídeo e, como `StageVideo` os objetos não estão na lista de exibição, o `viewPort` parâmetro contém as coordenadas absolutas do vídeo.
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

1. Atribua sua implementação à `MediaPlayerView` propriedade.

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. Adicione sua visualização à `view` propriedade do Media Player.

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

