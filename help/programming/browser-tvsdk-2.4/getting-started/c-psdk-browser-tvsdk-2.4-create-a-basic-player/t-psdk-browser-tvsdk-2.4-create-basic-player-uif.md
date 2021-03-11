---
title: Criar um reprodutor básico usando a Estrutura da interface do usuário
description: Criar um reprodutor básico usando a Estrutura da interface do usuário
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 1%

---


# Crie um reprodutor básico usando a Estrutura da interface do usuário{#create-a-basic-player-using-the-ui-framework}

Para criar um reprodutor básico usando a Estrutura da interface do usuário:

1. Crie um `<div>` para a instância do reprodutor.

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

   Quando o reprodutor é criado, o elemento `<div>` especificado recebe uma classe CSS `ptp-main-video-div-style`. O DOM resultante aparece assim:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. Adicionar um controle de interface do usuário.

   Por exemplo, adicione uma barra de controle que aparece quando o mouse passa sobre o player:

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

   O DOM resultante aparece da seguinte maneira:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <div class="ptp-control-bar my_control_bar"></div> 
       <video class="vp-video-element"></video> 
   </div>
   ```

O objeto retornado da chamada `ptp.videoPlayer()` fornece um comportamento que envolve a API do reprodutor de mídia TVSDK e permite o controle programático da reprodução. Quando você faz chamadas na instância do reprodutor de mídia, a interface do usuário é atualizada com base nos eventos acionados pelo reprodutor de mídia:

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
