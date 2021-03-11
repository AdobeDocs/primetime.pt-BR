---
description: A classe PlayerFragment é onde você edita o código para criar os gerentes de recursos totalmente habilitados.
title: PlayerFragment
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# PlayerFragment {#playerfragment}

A classe PlayerFragment é onde você edita o código para criar os gerentes de recursos totalmente habilitados.

A classe `PlayerFragment` contém todos os componentes da interface do usuário, como `playerFrame`, `ControlBar`, `playerClickableAdFragment` e `adOverlay`.

Ele lida com a inicialização de todos esses componentes, bem como com a criação do reprodutor, a configuração das exibições, a criação de gerenciadores de recursos para o reprodutor de mídia, o manuseio de eventos de mídia, como retomar, reproduzir e pausar e manipular os ouvintes de eventos para `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `PlaybackManager`.`AdsManager``EntitlementManager`

O arquivo XML que inclui os parâmetros de configuração para `PlayerFragment` é `res/layout/fragment_player.xml`.

Antes de criar os gerentes de recursos, você precisa criar o reprodutor de mídia, certificando-se de que o seguinte código esteja no arquivo `PlayerFragment.java`:

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
