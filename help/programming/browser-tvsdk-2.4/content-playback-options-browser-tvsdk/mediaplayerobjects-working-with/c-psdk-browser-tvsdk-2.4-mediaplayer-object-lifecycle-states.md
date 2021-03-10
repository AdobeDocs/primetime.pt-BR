---
description: A partir do momento em que a instância MediaPlayer é criada e terminada, essa instância é transferida de um estado para o seguinte.
title: Ciclo de vida e estados do objeto MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# Ciclo de vida e estados do objeto MediaPlayer{#life-cycle-and-states-of-the-mediaplayer-object}

A partir do momento em que a instância MediaPlayer é criada e terminada, essa instância é transferida de um estado para o seguinte.

Estes são os estados possíveis:

* **IDLE**:  `MediaPlayerStatus.IDLE`

* **INICIALIZAÇÃO**:  `MediaPlayerStatus.INITIALIZING`

* **INICIALIZADO**:  `MediaPlayerStatus.INITIALIZED`

* **PREPARANDO**:  `MediaPlayerStatus.PREPARING`

* **PREPARADO**:  `MediaPlayerStatus.PREPARED`

* **REPRODUZINDO**:  `MediaPlayerStatus.PLAYING`

* **PAUSADO**:  `MediaPlayerStatus.PAUSED`

* **BUSCA**:  `MediaPlayerStatus.SEEKING`

* **CONCLUIR**:  `MediaPlayerStatus.COMPLETE`

* **ERRO**:  `MediaPlayerStatus.ERROR`

* **LANÇADO**:  `MediaPlayerStatus.RELEASED`

A lista completa de estados é definida em `MediaPlayerStatus`.

Saber o estado do reprodutor é útil porque algumas operações são permitidas somente enquanto o reprodutor está em um estado específico. Por exemplo, `play` não pode ser chamado enquanto estiver no estado IDLE. Ele deve ser chamado depois de atingir o estado PREPARADO. O estado ERROR também altera o que pode acontecer em seguida.

Como um recurso de mídia é carregado e reproduzido, o reprodutor é transferido da seguinte maneira:

1. O estado inicial é IDLE.
1. Seu aplicativo chama `MediaPlayer.replaceCurrentResource`, o que move o reprodutor para o estado INICIALIZANDO.
1. Se o TVSDK do navegador carregar o recurso com êxito, o estado será alterado para INICIALIZADO.
1. Seu aplicativo chama `MediaPlayer.prepareToPlay` e o estado muda para PREPARING.
1. O TVSDK do navegador prepara o fluxo de mídia e inicia a resolução do anúncio e a inserção do anúncio (se ativada).

   Quando esta etapa é concluída, as publicidades são inseridas na linha do tempo ou o procedimento de anúncio falhou, e o estado do player muda para PREPARED.
1. Conforme seu aplicativo reproduz e pausa a mídia, o estado se move entre REPRODUZIR e PAUSADO.

   >[!TIP]
   >
   >Ao reproduzir ou pausar, ao sair da reprodução, desligar o dispositivo ou alternar os aplicativos, o estado é alterado para SUSPENDIDO e os recursos são lançados. Para continuar, restaure o reprodutor de mídia.

1. Quando o reprodutor atinge o fim do fluxo, o estado torna-se COMPLETE.
1. Quando seu aplicativo solta o reprodutor de mídia, o estado muda para LANÇADO.
1. Se ocorrer um erro durante o processo, o estado será alterado para ERROR.

Esta é uma ilustração do ciclo de vida de uma instância do MediaPlayer:

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

