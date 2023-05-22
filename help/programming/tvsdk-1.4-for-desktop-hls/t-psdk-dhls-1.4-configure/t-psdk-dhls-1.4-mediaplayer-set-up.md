---
description: A interface do MediaPlayer encapsula a funcionalidade e o comportamento de um reprodutor de mídia.
title: Configurar o MediaPlayer
exl-id: eec51f3e-4779-4fb5-b735-d5be412de64e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Configurar o MediaPlayer {#set-up-the-mediaplayer}

O TVSDK fornece ferramentas para criar um aplicativo de reprodutor de vídeo avançado (seu reprodutor do Primetime), que pode ser integrado a outros componentes do Primetime.

Use as ferramentas da plataforma para criar um reprodutor e conectá-lo à visualização do reprodutor de mídia no TVSDK, que tem métodos para reproduzir e gerenciar vídeos. Por exemplo, o TVSDK fornece métodos de reprodução e pausa. Você pode criar botões de interface do usuário em sua plataforma e definir os botões para chamar esses métodos TVSDK. A interface do MediaPlayer encapsula a funcionalidade e o comportamento de um reprodutor de mídia.

O TVSDK fornece uma única implementação do `MediaPlayer` interface: a classe DefaultMediaPlayer. Quando precisar da funcionalidade de reprodução de vídeo, crie uma instância `DefaultMediaPlayer`.

>[!NOTE]
>
>Interaja com o `DefaultMediaPlayer` instância somente com os métodos expostos pelo `MediaPlayer` interface.

1. Instanciar um `MediaPlayerContext` usando o aplicativo carregado `authorizedFeatures` instância (consulte [Carregar seu token assinado](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. Instanciar um `MediaPlayer` usando o método de criação de fábrica público, transmitindo um `MediaPlayerContext` objeto de contexto:

   ```
   public static function create(context:Context):MediaPlayer
   ```

   Isso retorna um valor `MediaPlayer` interface. 1. Instanciar um `MediaPlayerView` e especifique a ocorrência de StageVideo a ser usada:

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. Associe o `MediaPlayerView` instância com a exibição recém-criada:

   ```
   mediaPlayer.view = view;
   ```

1. Coloque o `MediaPlayerView` instância na tela do dispositivo:

   ```
   container.addChild(view)
   ```

A variável `MediaPlayer` A instância do agora está disponível e configurada corretamente para exibir conteúdo de vídeo na tela do dispositivo.
