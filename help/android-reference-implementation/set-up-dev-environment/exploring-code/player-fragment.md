---
description: A classe PlayerFragment é onde você edita o código para criar gerenciadores de recursos totalmente ativados.
title: PlayerFragment
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# PlayerFragment {#playerfragment}

A classe PlayerFragment é onde você edita o código para criar gerenciadores de recursos totalmente ativados.

A variável `PlayerFragment` A classe contém todos os componentes da interface do usuário, como o `playerFrame`, `ControlBar`, `playerClickableAdFragment`, e `adOverlay`.

Ele lida com a inicialização de todos esses componentes, além de criar o reprodutor, configurar as exibições, criar gerenciadores de recursos para o reprodutor de mídia, lidar com eventos de mídia como retomar, reproduzir e pausar, além de lidar com os ouvintes de eventos para `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `AdsManager`, `PlaybackManager`, e `EntitlementManager`.

O arquivo XML que inclui os parâmetros de configuração para o `PlayerFragment` é `res/layout/fragment_player.xml`.

Antes de criar os gerenciadores de recursos, é necessário criar o reprodutor de mídia verificando se o código a seguir está na `PlayerFragment.java` arquivo:

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
