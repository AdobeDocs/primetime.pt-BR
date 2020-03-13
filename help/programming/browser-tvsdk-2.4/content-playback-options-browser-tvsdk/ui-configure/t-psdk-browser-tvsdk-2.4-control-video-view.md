---
description: É possível controlar a posição e o tamanho da exibição de vídeo usando o objeto MediaPlayerView.
seo-description: É possível controlar a posição e o tamanho da exibição de vídeo usando o objeto MediaPlayerView.
seo-title: Controlar a posição e o tamanho da visualização de vídeo
title: Controlar a posição e o tamanho da visualização de vídeo
uuid: d09dbc18-1ec0-4336-bf3f-7ff6c265c443
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Controlar a posição e o tamanho da visualização de vídeo{#control-the-position-and-size-of-the-video-view}

É possível controlar a posição e o tamanho da exibição de vídeo usando o objeto MediaPlayerView.

Por padrão, o TVSDK do navegador tenta manter a proporção da exibição do vídeo sempre que o tamanho ou a posição do vídeo se altera devido a uma alteração feita pelo aplicativo, uma alteração de perfil, uma alteração de conteúdo e assim por diante.

Você pode substituir o comportamento padrão de proporção especificando uma política *de* escala diferente. Especifique a política de escala usando a propriedade do `MediaPlayerView` objeto `scalePolicy` . A política de escala padrão de `MediaPlayerView` é definida com uma instância da `MaintainAspectRatioScalePolicy` classe. Para redefinir a política de escala, substitua a instância padrão de `MaintainAspectRatioScalePolicy` on por `MediaPlayerView.scalePolicy` sua própria política.

>[!IMPORTANT]
>
>Não é possível definir a `scalePolicy` propriedade como um valor nulo.

## Cenários de fallback não Flash {#non-flash-fallback-scenarios}

Em cenários de fallback não Flash, para que a política de escala funcione corretamente, o elemento div de vídeo fornecido no `View` construtor deve retornar valores diferentes de zero para `offsetWidth` e `offsetHeight`. Para dar um exemplo de função incorreta, às vezes, quando a largura e a altura dos elementos div do vídeo não são definidos explicitamente em css, o `View` construtor retorna zero para `offsetWidth` ou `offsetHeight`.

>[!NOTE]
>
>O CustomScalePolicy tem suporte limitado para alguns navegadores, como IE, Edge e Safari 9. Para esses navegadores, a proporção de aspecto nativa do vídeo não pode ser alterada. No entanto, a posição e as dimensões do vídeo serão aplicadas de acordo com a política de escala.

1. Implemente a `MediaPlayerViewScalePolicy` interface para criar sua própria política de escala.

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

1. Atribua sua implementação à `MediaPlayerView` propriedade.

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. Adicione sua exibição à `view` propriedade do Media Player.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**Por exemplo: Dimensione o vídeo para preencher toda a exibição do vídeo, sem manter a proporção:**

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

