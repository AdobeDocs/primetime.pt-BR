---
description: A interface do MediaPlayer encapsula a funcionalidade e o comportamento de um player de mídia.
seo-description: A interface do MediaPlayer encapsula a funcionalidade e o comportamento de um player de mídia.
seo-title: Configurar o MediaPlayer
title: Configurar o MediaPlayer
uuid: 4b27643c-9ccd-4abb-9793-475d06ee2a88
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Configurar o MediaPlayer {#set-up-the-mediaplayer}

O TVSDK fornece ferramentas para a criação de um aplicativo de player de vídeo avançado (seu player do Primetime), que pode ser integrado a outros componentes do Primetime.

Use as ferramentas da sua plataforma para criar um player e conectá-lo à exibição do player de mídia no TVSDK, que tem métodos para reproduzir e gerenciar vídeos. Por exemplo, o TVSDK fornece métodos de reprodução e pausa. Você pode criar botões da interface do usuário em sua plataforma e definir os botões para chamar esses métodos TVSDK. A interface do MediaPlayer encapsula a funcionalidade e o comportamento de um player de mídia.

O TVSDK fornece uma única implementação da `MediaPlayer` interface: a classe DefaultMediaPlayer. Quando precisar da funcionalidade de reprodução de vídeo, instancie `DefaultMediaPlayer`.

>[!NOTE]
>
>Interaja com a `DefaultMediaPlayer` instância somente com os métodos expostos pela `MediaPlayer` interface.

1. Instancie um `MediaPlayerContext` usando a `authorizedFeatures` instância carregada pelo aplicativo (consulte [Carregar seu token](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)assinado).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. Instancie um método `MediaPlayer` de criação de fábrica pública, transmitindo um objeto de `MediaPlayerContext` contexto:

   ```
   public static function create(context:Context):MediaPlayer
   ```

   Isso retorna uma `MediaPlayer` interface genérica. 1. Instancie um `MediaPlayerView` e especifique a instância StageVideo a ser usada:

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. Associe a `MediaPlayerView` instância à exibição recém-criada:

   ```
   mediaPlayer.view = view;
   ```

1. Coloque a `MediaPlayerView` instância na tela do dispositivo:

   ```
   container.addChild(view)
   ```

A `MediaPlayer` instância agora está disponível e corretamente configurada para exibir o conteúdo de vídeo na tela do dispositivo.