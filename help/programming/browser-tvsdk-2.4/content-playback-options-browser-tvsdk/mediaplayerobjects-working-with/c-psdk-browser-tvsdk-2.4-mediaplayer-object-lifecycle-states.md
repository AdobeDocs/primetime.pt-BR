---
description: A partir do momento em que a ocorrência de MediaPlayer é criada até o momento em que é encerrada, essa ocorrência passa de um estado para o próximo.
title: Ciclo de vida e estados do objeto MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# Ciclo de vida e estados do objeto MediaPlayer{#life-cycle-and-states-of-the-mediaplayer-object}

A partir do momento em que a ocorrência de MediaPlayer é criada até o momento em que é encerrada, essa ocorrência passa de um estado para o próximo.

Estes são os estados possíveis:

* **OCIOSO**: `MediaPlayerStatus.IDLE`

* **INICIALIZANDO**: `MediaPlayerStatus.INITIALIZING`

* **INICIALIZADO**: `MediaPlayerStatus.INITIALIZED`

* **PREPARANDO**: `MediaPlayerStatus.PREPARING`

* **PREPARADO**: `MediaPlayerStatus.PREPARED`

* **REPRODUÇÃO**: `MediaPlayerStatus.PLAYING`

* **PAUSADO**: `MediaPlayerStatus.PAUSED`

* **BUSCANDO**: `MediaPlayerStatus.SEEKING`

* **CONCLUÍDO**: `MediaPlayerStatus.COMPLETE`

* **ERRO**: `MediaPlayerStatus.ERROR`

* **LANÇADO**: `MediaPlayerStatus.RELEASED`

A lista completa de estados é definida em `MediaPlayerStatus`.

Conhecer o estado do reprodutor é útil porque algumas operações são permitidas somente enquanto o reprodutor está em um estado específico. Por exemplo, `play` não pode ser chamado enquanto estiver no estado IDLE. Ele deve ser chamado depois de atingir o estado PREPARADO. O estado ERROR também altera o que pode acontecer a seguir.

À medida que um recurso de mídia é carregado e reproduzido, o reprodutor faz a transição da seguinte maneira:

1. O estado inicial é IDLE.
1. Suas chamadas de aplicativo `MediaPlayer.replaceCurrentResource`, que move o reprodutor para o estado INICIALIZANDO.
1. Se o TVSDK do navegador carregar o recurso com êxito, o estado será alterado para INITIALIZED.
1. Suas chamadas de aplicativo `MediaPlayer.prepareToPlay`, e o estado será alterado para PREPARANDO.
1. O TVSDK do navegador prepara o fluxo de mídia e inicia a resolução do anúncio e a inserção do anúncio (se ativada).

   Quando essa etapa é concluída, os anúncios são inseridos na linha do tempo ou o procedimento de anúncio falha e o estado do player muda para PREPARED.
1. Conforme o aplicativo é reproduzido e pausa a mídia, o estado se move entre REPRODUZINDO e PAUSADO.

   >[!TIP]
   >
   >Durante a reprodução ou em pausa, quando você sai da reprodução, encerra o dispositivo ou troca de aplicativos, o estado muda para SUSPENSO e os recursos são liberados. Para continuar, restaure o reprodutor de mídia.

1. Quando o reprodutor atinge o final do fluxo, o estado se torna COMPLETE.
1. Quando o aplicativo libera o reprodutor de mídia, o estado muda para LIBERADO.
1. Se ocorrer um erro durante o processo, o estado será alterado para ERROR.

Esta é uma ilustração do ciclo de vida de uma ocorrência de MediaPlayer:

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

Você pode usar o estado para fornecer feedback ao usuário sobre o processo (por exemplo, um ponteiro enquanto aguarda a próxima alteração de estado) ou para tomar as próximas etapas na reprodução da mídia, como aguardar o estado apropriado antes de chamar o próximo método.

Por exemplo:

```js
function onStateChanged(state) { 
    switch(state) { 
        // It is recommended that you call prepareToPlay()  
        // after receiving the INITIALIZED state             
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            mediaPlayer.prepareToPlay(); 
            break; 
    } 
} 
```
