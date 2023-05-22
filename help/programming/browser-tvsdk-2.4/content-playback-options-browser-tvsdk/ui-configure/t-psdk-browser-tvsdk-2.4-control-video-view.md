---
description: É possível controlar a posição e o tamanho da visualização do vídeo usando o objeto MediaPlayerView.
title: Controlar a posição e o tamanho da visualização do vídeo
exl-id: ab88a90f-4493-4f05-8da0-703ab3cf159e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Controlar a posição e o tamanho da visualização do vídeo{#control-the-position-and-size-of-the-video-view}

É possível controlar a posição e o tamanho da visualização do vídeo usando o objeto MediaPlayerView.

Por padrão, o TVSDK do navegador tenta manter a proporção da visualização de vídeo sempre que o tamanho ou a posição do vídeo é alterado devido a uma alteração feita pelo aplicativo, uma alteração de perfil, uma alteração de conteúdo e assim por diante.

Você pode substituir o comportamento padrão da taxa de proporção especificando uma opção *política de escala*. Especifique a política de escala usando o `MediaPlayerView` do objeto `scalePolicy` propriedade. A política de escala padrão de `MediaPlayerView` é definido com uma instância do `MaintainAspectRatioScalePolicy` classe. Para redefinir a política de escala, substitua a instância padrão de `MaintainAspectRatioScalePolicy` em `MediaPlayerView.scalePolicy` com sua própria política.

>[!IMPORTANT]
>
>Você não pode definir a variável `scalePolicy` a um valor nulo.

## Cenários de fallback sem Flash {#non-flash-fallback-scenarios}

Em cenários de fallback sem Flash, para que a política de escala funcione corretamente, o elemento video div fornecido no `View` o construtor deve retornar valores diferentes de zero para `offsetWidth` e `offsetHeight`. Para fornecer um exemplo de função incorreta, às vezes, quando a largura e a altura dos elementos div do vídeo não estão definidas explicitamente no css, a variável `View` construtor retorna zero para `offsetWidth` ou `offsetHeight`.

>[!NOTE]
>
>O CustomScalePolicy tem suporte limitado para alguns navegadores, principalmente IE, Edge e Safari 9. Nesses navegadores, a proporção nativa do vídeo não pode ser alterada. No entanto, a posição e as dimensões do vídeo serão aplicadas de acordo com a política de escala.

1. Implementar o `MediaPlayerViewScalePolicy` para criar sua própria política de escala.

   A variável `MediaPlayerViewScalePolicy` tem um método:

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

1. Atribua sua implementação ao `MediaPlayerView` propriedade.

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. Adicionar sua visualização ao do reprodutor de mídia `view` propriedade.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**Por exemplo: dimensione o vídeo para preencher toda a exibição de vídeo, sem manter a taxa de proporção:**

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
