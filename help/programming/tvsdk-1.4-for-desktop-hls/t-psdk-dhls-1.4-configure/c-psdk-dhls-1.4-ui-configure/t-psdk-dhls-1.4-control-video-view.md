---
description: É possível controlar a posição e o tamanho da visualização do vídeo usando o objeto MediaPlayerView.
title: Controlar a posição e o tamanho da visualização do vídeo
exl-id: 5e7ae557-7f2b-4697-85eb-e72d1f43a7fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Controlar a posição e o tamanho da visualização do vídeo{#control-the-position-and-size-of-the-video-view}

É possível controlar a posição e o tamanho da visualização do vídeo usando o objeto MediaPlayerView.

O TVSDK tenta, por padrão, manter a proporção da visualização de vídeo sempre que o tamanho ou a posição do vídeo são alterados (devido a uma alteração feita pelo aplicativo, ou por uma troca de perfil, ou uma troca de conteúdo etc.).

Você pode substituir o comportamento padrão da taxa de proporção especificando uma opção *política de escala*. Especifique a política de escala usando o `MediaPlayerView` do objeto `scalePolicy` propriedade. A variável `MediaPlayerView`A política de escala padrão do é definida com uma instância do `MaintainAspectRatioScalePolicy` classe. Para redefinir a política de escala, substitua a instância padrão de `MaintainAspectRatioScalePolicy` em `MediaPlayerView.scalePolicy` com sua própria política. (Você não pode definir a variável `scalePolicy` para um valor nulo.)

1. Implementar o `MediaPlayerViewScalePolicy` para criar sua própria política de escala.

   A variável `MediaPlayerViewScalePolicy` tem um método:

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >O TVSDK usa um `StageVideo` para exibir o vídeo e porque `StageVideo` objetos não estiverem na lista de exibição, a variável `viewPort` contém as coordenadas absolutas do vídeo.
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

1. Atribua sua implementação ao `MediaPlayerView` propriedade.

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. Adicionar sua visualização ao do reprodutor de mídia `view` propriedade.

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**Por exemplo: dimensione o vídeo para preencher toda a exibição de vídeo, sem manter a taxa de proporção:**

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
