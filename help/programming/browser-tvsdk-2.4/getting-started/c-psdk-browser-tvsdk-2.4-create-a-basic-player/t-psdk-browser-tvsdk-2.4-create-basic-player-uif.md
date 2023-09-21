---
title: Criar um player básico usando a Estrutura da interface
description: Criar um player básico usando a Estrutura da interface
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# Criar um player básico usando a Estrutura da interface{#create-a-basic-player-using-the-ui-framework}

Para criar um reprodutor básico usando a Estrutura da interface:

1. Criar um `<div>` para sua instância do reprodutor.

   Por exemplo:

   ```
   <div id="video1" > 
    </div>
   ```

1. Carregue o reprodutor.

   ```js
   <script> 
       (function(){ 
           var player = ptp.videoPlayer('#video1'); 
       })(); 
   </script>
   ```

   Quando o reprodutor é criado, o `<div>` elemento recebe uma classe CSS de `ptp-main-video-div-style`. O DOM resultante aparece assim:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. Adicionar um controle da interface do usuário.

   Por exemplo, adicione uma barra de controle que aparece quando o mouse passa sobre o reprodutor:

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

O objeto retornou da chamada `ptp.videoPlayer()` O fornece um comportamento que envolve a API do reprodutor de mídia TVSDK e permite o controle programático da reprodução. Quando você faz chamadas na instância do reprodutor de mídia, a interface do usuário se atualiza com base nos eventos acionados pelo reprodutor de mídia:

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
