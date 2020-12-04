---
description: A classe PlayerFragment é onde você edita o código para criar os gerenciadores de recursos totalmente habilitados.
seo-description: A classe PlayerFragment é onde você edita o código para criar os gerenciadores de recursos totalmente habilitados.
seo-title: PlayerFragment
title: PlayerFragment
uuid: 83f02c31-f3b1-4d16-97c8-5b391e8c999a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# PlayerFragment {#playerfragment}

A classe PlayerFragment é onde você edita o código para criar os gerenciadores de recursos totalmente habilitados.

A classe `PlayerFragment` contém todos os componentes da interface do usuário, como `playerFrame`, `ControlBar`, `playerClickableAdFragment` e `adOverlay`.

Ele trata da inicialização de todos esses componentes, além de criar o player, configurar o visualização, criar gerenciadores de recursos para o player de mídia, manipular eventos de mídia como retomar, reproduzir e pausar e manipular os ouvintes de evento para `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `AdsManager`, `PlaybackManager` e `EntitlementManager`.

O arquivo XML que inclui os parâmetros de configuração para `PlayerFragment` é `res/layout/fragment_player.xml`.

Antes de criar os gerenciadores de recursos, é necessário criar o player de mídia, certificando-se de que o seguinte código esteja no arquivo `PlayerFragment.java`:

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
