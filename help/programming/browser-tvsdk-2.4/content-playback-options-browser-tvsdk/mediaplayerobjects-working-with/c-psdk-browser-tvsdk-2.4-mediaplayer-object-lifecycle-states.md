---
description: A partir do momento em que a instância MediaPlayer é criada até o momento em que é encerrada, essa instância transição de um estado para o seguinte.
seo-description: A partir do momento em que a instância MediaPlayer é criada até o momento em que é encerrada, essa instância transição de um estado para o seguinte.
seo-title: Ciclo de vida e estados do objeto MediaPlayer
title: Ciclo de vida e estados do objeto MediaPlayer
uuid: fe76ea80-aaa8-43bc-9b81-85e0551f70dd
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# Ciclo de vida e estados do objeto MediaPlayer{#life-cycle-and-states-of-the-mediaplayer-object}

A partir do momento em que a instância MediaPlayer é criada até o momento em que é encerrada, essa instância transição de um estado para o seguinte.

Estes são os estados possíveis:

* **IDLE**:  `MediaPlayerStatus.IDLE`

* **INICIALIZAÇÃO**:  `MediaPlayerStatus.INITIALIZING`

* **INICIALIZADO**:  `MediaPlayerStatus.INITIALIZED`

* **PREPARANDO**:  `MediaPlayerStatus.PREPARING`

* **PREPARADO**:  `MediaPlayerStatus.PREPARED`

* **REPRODUÇÃO**:  `MediaPlayerStatus.PLAYING`

* **PAUSADO**:  `MediaPlayerStatus.PAUSED`

* **PROCURANDO**:  `MediaPlayerStatus.SEEKING`

* **CONCLUÍDO**:  `MediaPlayerStatus.COMPLETE`

* **ERRO**:  `MediaPlayerStatus.ERROR`

* **LANÇADO**:  `MediaPlayerStatus.RELEASED`

A lista completa de estados é definida em `MediaPlayerStatus`.

Saber o estado do player é útil porque algumas operações são permitidas apenas enquanto o player estiver em um estado específico. Por exemplo, `play` não pode ser chamado enquanto estiver no estado IDLE. Deve ser chamado depois de chegar ao estado PREPARADO. O estado ERROR também muda o que pode acontecer a seguir.

Como um recurso de mídia é carregado e reproduzido, o player transição da seguinte maneira:

1. O estado inicial é IDLE.
1. Seu aplicativo chama `MediaPlayer.replaceCurrentResource`, que move o player para o estado INICIALIZANDO.
1. Se o TVSDK do navegador carregar o recurso com êxito, o estado mudará para INICIALIZADO.
1. Seu aplicativo chama `MediaPlayer.prepareToPlay` e o estado muda para PREPARING.
1. O TVSDK do navegador prepara o fluxo de mídia e start a resolução do anúncio e a inserção do anúncio (se ativada).

   Quando essa etapa for concluída, os anúncios serão inseridos na linha do tempo ou o procedimento do anúncio falhará e o estado do player mudará para PREPARADO.
1. Conforme seu aplicativo é reproduzido e pausa a mídia, o estado se move entre REPRODUZIR e PAUSADO.

   >[!TIP]
   >
   >Durante a reprodução ou pausada, quando você navega para fora da reprodução, desliga o dispositivo ou alterna os aplicativos, o estado muda para SUSPENDED e os recursos são liberados. Para continuar, restaure o player de mídia.

1. Quando o player atinge o final do fluxo, o estado se torna COMPLETE.
1. Quando seu aplicativo solta o player de mídia, o estado muda para LIBERADO.
1. Se ocorrer um erro durante o processo, o estado mudará para ERRO.

Esta é uma ilustração do ciclo de vida de uma instância do MediaPlayer:

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

Você pode usar o estado para fornecer feedback ao usuário sobre o processo (por exemplo, uma roleta enquanto espera pela próxima alteração de estado) ou para executar as próximas etapas na mídia, como aguardar o estado apropriado antes de chamar o próximo método.

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

