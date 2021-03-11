---
description: A interface PTMediaPlayer encapsula a funcionalidade e o comportamento de um objeto do reprodutor de mídia.
title: Configurar o PTMediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Configurar o PTMediaPlayer {#set-up-the-ptmediaplayer}

O TVSDK fornece ferramentas para criar um aplicativo de reprodutor de vídeo avançado (seu reprodutor Primetime), que pode ser integrado a outros componentes do Primetime.

Use as ferramentas da plataforma para criar um reprodutor e conectá-lo à exibição do reprodutor de mídia no TVSDK, que tem métodos para reproduzir e gerenciar vídeos. Por exemplo, o TVSDK fornece métodos de reprodução e pausa. Você pode criar botões da interface do usuário na sua plataforma e definir os botões para chamar esses métodos TVSDK.

A interface PTMediaPlayer encapsula a funcionalidade e o comportamento de um objeto do reprodutor de mídia.

Para configurar seu `PTMediaPlayer`:

1. Busque o URL da mídia na interface do usuário, por exemplo, em um campo de texto.

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. Crie `PTMetadata`.

   Suponha que seu método `createMetada` prepare metadados (consulte [Advertising](../ad-insertion/r-psdk-ios-1.4-advertising-requirements.md)).

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

1. Defina a propriedade view do reprodutor.

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
   
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. Adicione a exibição do reprodutor na subexibição atual.

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. Chame `play` para iniciar a reprodução de mídia.

   ```
   [player play];
   ```

