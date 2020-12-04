---
description: A interface PTMediaPlayer encapsula a funcionalidade e o comportamento de um objeto de player de mídia.
seo-description: A interface PTMediaPlayer encapsula a funcionalidade e o comportamento de um objeto de player de mídia.
seo-title: Configurar o PTMediaPlayer
title: Configurar o PTMediaPlayer
uuid: 78549406-7e33-4bca-a25e-1e433f6a75d7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Configurar PTMediaPlayer {#set-up-the-ptmediaplayer}

O TVSDK fornece ferramentas para a criação de um aplicativo de player de vídeo avançado (seu player do Primetime), que pode ser integrado a outros componentes do Primetime.

Use as ferramentas da sua plataforma para criar um player e conectá-lo à visualização do player de mídia no TVSDK, que tem métodos para reproduzir e gerenciar vídeos. Por exemplo, o TVSDK fornece métodos de reprodução e pausa. Você pode criar botões da interface do usuário na plataforma e definir os botões para chamar esses métodos TVSDK.

A interface PTMediaPlayer encapsula a funcionalidade e o comportamento de um objeto de player de mídia.

Para configurar seu `PTMediaPlayer`:

1. Procure o URL da mídia na interface do usuário, por exemplo, em um campo de texto.

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. Crie `PTMetadata`.

   Suponha que seu método `createMetada` prepare metadados (consulte [Publicidade](../ad-insertion/r-psdk-ios-1.4-advertising-requirements.md)).

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. Crie `PTMediaPlayerItem` usando sua instância `PTMetadata`.

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. Adicione observadores a notificações que o TVSDK envia.

   ```
   [self addObservers]
   ```

1. Crie `PTMediaPlayer` usando seu novo `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. Defina as propriedades no player.

   Estas são algumas das propriedades `PTMediaPlayer` disponíveis:

   ```
   player.autoPlay                    = YES;  
   player.closedCaptionDisplayEnabled = YES; 
   player.videoGravity                = PTMediaPlayerVideoGravityResizeAspect;  
   player.allowsAirPlayVideo          = YES;
   ```

1. Defina a propriedade de visualização do player.

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
   
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. Adicione a visualização do player na subexibição atual da visualização.

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. Chame `play` para a reprodução de mídia de start.

   ```
   [player play];
   ```

