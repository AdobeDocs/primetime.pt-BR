---
description: A interface do PTMediaPlayer encapsula a funcionalidade e o comportamento de um objeto do reprodutor de mídia.
title: Configurar o PTMediaPlayer
exl-id: cf8f46c8-c52a-4f44-b493-965ce1b50c68
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Configurar o PTMediaPlayer {#set-up-the-ptmediaplayer}

O TVSDK fornece ferramentas para criar um aplicativo de reprodutor de vídeo avançado (seu reprodutor do Primetime), que pode ser integrado a outros componentes do Primetime.

Use as ferramentas da plataforma para criar um reprodutor e conectá-lo à visualização do reprodutor de mídia no TVSDK, que tem métodos para reproduzir e gerenciar vídeos. Por exemplo, o TVSDK fornece métodos de reprodução e pausa. Você pode criar botões de interface do usuário na plataforma e definir os botões para chamar esses métodos TVSDK.

A interface do PTMediaPlayer encapsula a funcionalidade e o comportamento de um objeto do reprodutor de mídia.

Para configurar o seu `PTMediaPlayer`:

1. Busque o URL da mídia na interface do usuário, por exemplo, em um campo de texto.

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. Criar `PTMetadata`.

   Suponha que seu método `createMetada` prepara metadados (consulte [Publicidade](../ad-insertion/r-psdk-ios-1.4-advertising-requirements.md)).

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. Criar `PTMediaPlayerItem` usando o seu `PTMetadata` instância.

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. Adicione observadores a notificações que o TVSDK despacha.

   ```
   [self addObservers]
   ```

1. Criar `PTMediaPlayer` usar seu novo `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. Definir propriedades no reprodutor.

   Aqui estão algumas das disponíveis `PTMediaPlayer` propriedades:

   ```
   player.autoPlay                    = YES;  
   player.closedCaptionDisplayEnabled = YES; 
   player.videoGravity                = PTMediaPlayerVideoGravityResizeAspect;  
   player.allowsAirPlayVideo          = YES;
   ```

1. Defina a propriedade de visualização do reprodutor.

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
   
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. Adicionar a visualização do reprodutor na subvisualização da visualização atual.

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. Chame `play` para iniciar a reprodução de mídia.

   ```
   [player play];
   ```
