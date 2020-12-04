---
description: nulo
seo-description: nulo
seo-title: Criar um player básico usando a Estrutura da interface do usuário
title: Criar um player básico usando a Estrutura da interface do usuário
uuid: d1a82dbb-1c05-4d0c-b6bc-e07cbede93cb
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 1%

---


# Crie um player básico usando a Estrutura da interface{#create-a-basic-player-using-the-ui-framework}

Para criar um player básico usando a Estrutura da interface do usuário:

1. Crie um `<div>` para a instância do player.

   Por exemplo:

   ```
   <div id="video1" > 
    </div>
   ```

1. Carregue o player.

   ```js
   <script> 
       (function(){ 
           var player = ptp.videoPlayer('#video1'); 
       })(); 
   </script>
   ```

   Quando o player é criado, o elemento `<div>` especificado recebe uma classe CSS de `ptp-main-video-div-style`. O DOM resultante é semelhante a:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. Adicione um controle de interface do usuário.

   Por exemplo, adicione uma barra de controle que aparece quando o mouse passa o mouse sobre o player:

   ```js
   <script> 
       (function(){ 
           function myControlBarBehavior(element, configuration, player) { 
               return ptp.controlBarBehavior(element, configuration, player); 
           } 
           var player = ptp.videoPlayer('#video1', { 
               controlBar: { 
                   behavior: myControlBarBehavior, 
                   classNames: 'ptp-control-bar my_control_bar' 
               } 
           }); 
       })(); 
   </script>
   ```

   O DOM resultante é exibido da seguinte maneira:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <div class="ptp-control-bar my_control_bar"></div> 
       <video class="vp-video-element"></video> 
   </div>
   ```

O objeto retornado da chamada `ptp.videoPlayer()` fornece um comportamento que envolve a API do player de mídia TVSDK e permite o controle programático da reprodução. Quando você efetua chamadas na instância do player de mídia, a interface do usuário atualiza-se com base em eventos acionados pelo player de mídia:

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
