---
description: É possível controlar a posição e o tamanho da visualização de vídeo usando o objeto MediaPlayerView.
seo-description: É possível controlar a posição e o tamanho da visualização de vídeo usando o objeto MediaPlayerView.
seo-title: Controlar a posição e o tamanho da visualização de vídeo
title: Controlar a posição e o tamanho da visualização de vídeo
uuid: d09dbc18-1ec0-4336-bf3f-7ff6c265c443
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Controlar a posição e o tamanho da visualização de vídeo{#control-the-position-and-size-of-the-video-view}

É possível controlar a posição e o tamanho da visualização de vídeo usando o objeto MediaPlayerView.

Por padrão, o TVSDK do navegador tenta manter a proporção da visualização de vídeo sempre que o tamanho ou a posição do vídeo mudam devido a uma alteração feita pelo aplicativo, um switch de perfil, uma mudança de conteúdo e assim por diante.

Você pode substituir o comportamento padrão de proporção especificando uma *política de escala* diferente. Especifique a política de escala usando a propriedade `MediaPlayerView` do objeto `scalePolicy`. A política de escala padrão de `MediaPlayerView` é definida com uma instância da classe `MaintainAspectRatioScalePolicy`. Para redefinir a política de escala, substitua a instância padrão de `MaintainAspectRatioScalePolicy` em `MediaPlayerView.scalePolicy` por sua própria política.

>[!IMPORTANT]
>
>Não é possível definir a propriedade `scalePolicy` como um valor nulo.

## Cenários de fallback sem Flash {#non-flash-fallback-scenarios}

Em cenários de fallback que não sejam de Flash, para que a política de dimensionamento funcione corretamente, o elemento div de vídeo fornecido no construtor `View` deve retornar valores diferentes de zero para `offsetWidth` e `offsetHeight`. Para dar um exemplo de função incorreta, às vezes quando a largura e a altura dos elementos div de vídeo não estão definidos explicitamente em css, o construtor `View` retorna zero para `offsetWidth` ou `offsetHeight`.

>[!NOTE]
>
>O CustomScalePolicy tem suporte limitado para alguns navegadores, como IE, Edge e Safari 9. Para esses navegadores, a proporção de aspecto nativa do vídeo não pode ser alterada. No entanto, a posição e as dimensões do vídeo serão aplicadas de acordo com a política de escala.

1. Implemente a interface `MediaPlayerViewScalePolicy` para criar sua própria política de escala.

   O `MediaPlayerViewScalePolicy` tem um método:

   ```js
   /** 
   * Adjust the specified rectangle to match the new video dimensions. 
   * @param viewPort {AdobePSDK.Rectangle}The video rectangle as absolute position. 
   * @param videoWidth {Number}The video width. 
   * @param videoHeight {Number} The video height. 
   * @return {AdobePSDK.Rectangle} an adjusted rectangle. 
   */ 
   function adjustCallbackFunc(viewPort, videoWidth, videoHeight);
   ```

   Por exemplo:

   ```js
   /** 
   Default Constructor 
   */ 
   MediaPlayerViewCustomScalePolicy = function() { 
       return this; 
   }; 
   MediaPlayerViewCustomScalePolicy.prototype = { 
       constructor: MediaPlayerViewScalePolicy, 
       adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
           /* Your Custom Adjustment here. */ 
           [...] 
           return adjustedRectangle; 
       } 
   };
   ```

1. Atribua sua implementação à propriedade `MediaPlayerView`.

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. Adicione sua visualização à propriedade `view` do Media Player.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**Por exemplo: Dimensione o vídeo para preencher a visualização de vídeo inteira, sem manter a proporção:**

```
/** 
 * Default constructor. 
 */ 
MediaPlayerViewCustomScalePolicy = function() { 
    return this; 
}; 
MediaPlayerViewCustomScalePolicy.prototype = { 
    constructor: MediaPlayerViewScalePolicy, 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
        return viewPort; 
    } 
}; 
var view = new AdobePSDK.MediaPlayerView(videoDiv); 
view.scalePolicy = new MediaPlayerViewCustomScalePolicy (); 
mediaPlayer.view = view;
```

