---
description: A inserção de anúncio resolve os anúncios de VOD (video-on-demand) , para transmissão ao vivo e para transmissão linear com rastreamento de anúncios e reprodução de anúncios. O TVSDK faz as solicitações necessárias para o servidor de publicidade, recebe informações sobre anúncios para o conteúdo especificado e coloca os anúncios em fases.
title: Inserir anúncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Inserir anúncios{#insert-ads}

A inserção de anúncio resolve os anúncios de VOD (video-on-demand) , para transmissão ao vivo e para transmissão linear com rastreamento de anúncios e reprodução de anúncios. O TVSDK faz as solicitações necessárias para o servidor de publicidade, recebe informações sobre anúncios para o conteúdo especificado e coloca os anúncios em fases.

Um *`ad break`* contém um ou mais anúncios que são exibidos em sequência. O TVSDK insere anúncios no conteúdo principal como membros de um ou mais ad breaks.

>[!TIP]
>
>Se o anúncio tiver erros, o TVSDK ignorará o anúncio.

## Resolver e inserir anúncios VOD {#section_157344F857C64F36B48AD441F6E7FABA}

O TVSDK oferece suporte a vários casos de uso para solução e inserção de anúncios VOD.

* Inserção de anúncio precedente, onde os anúncios são inseridos no início do conteúdo.
* Inserção de anúncio intermediário, onde pelo menos um anúncio é inserido no meio do conteúdo.
* Inserção de anúncio posterior, em que pelo menos um anúncio é anexado ao final do conteúdo.

O TVSDK resolve os anúncios, insere os anúncios em locais definidos pelo servidor de anúncios e calcula a linha do tempo virtual antes do início da reprodução. Após o início da reprodução, nenhuma alteração, como anúncios sendo inseridos ou anúncios inseridos sendo removidos, pode ocorrer.

## Resolva e insira anúncios em tempo real e linear {#section_A6A1BB262D084462A1D134083556B7CC}

O TVSDK oferece suporte a vários casos de uso para a resolução e inserção de anúncios em tempo real e linear.

* Inserção de anúncio precedente, em que pelo menos um anúncio é inserido no início do conteúdo.
* Inserção de anúncio intermediário, onde pelo menos um anúncio é inserido no meio do conteúdo.

O TVSDK resolve os anúncios e insere os anúncios quando um ponto de sinalização é encontrado no fluxo ao vivo ou linear. Por padrão, o TVSDK oferece suporte às seguintes dicas como marcadores de anúncios válidos ao resolver e inserir anúncios:

* # EXT-X-CUEPOINT
* # EXT-X-AD
* # EXT-X-CUE
* # EXT-X-CUE-OUT

Esses marcadores exigem o `DURATION` do campo de metadados em segundos e a ID exclusiva da sinalização. Por exemplo:

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

Para obter mais informações sobre dicas adicionais, consulte [Assinar tags personalizadas](../ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-custom-tags-subscribe.md).

## Rastrear anúncio de cliente {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

O TVSDK rastreia automaticamente anúncios para transmissão VOD e transmissão ao vivo/linear.

As notificações são usadas para informar seu aplicativo sobre o progresso de um anúncio, incluindo informações sobre quando ele começa e quando termina.

## Implementar um retorno antecipado de ad break {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

Para a inserção de um anúncio em stream ao vivo, talvez seja necessário sair de um ad break antes que todos os anúncios no break sejam reproduzidos até o fim.

Estes são alguns exemplos de retorno antecipado de ad break:

* A duração do ad break em determinados eventos esportivos.

   Embora uma duração padrão seja fornecida, se o jogo for retomado antes da interrupção ser concluída, o ad break deverá ser encerrado.
* Um sinal de emergência durante uma interrupção de anúncio em um stream ao vivo.

A capacidade de sair de um ad break precocemente é identificada por meio de uma tag personalizada no manifesto conhecida como um splice-in ou uma tag de cue-in. O TVSDK permite que o aplicativo assine essas tags de separação para fornecer uma oportunidade de divisão.

* Para usar a tag `#EXT-X-CUE-IN` como uma oportunidade de separação e implementar um retorno antecipado de ad break:

   1. Assine a tag .

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. Adicione o resolvedor de oportunidade de cue-in.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* Para compartilhar a mesma tag para splice-out e splice-in:

   1. Se o aplicativo estiver compartilhando a mesma dica para indicar cue-out/splice-out e cue-in/splice-in, estenda `PTDefaultAdOpportunityResolver` e implemente o método `preparePlacementOpportunity`.

      >[!TIP]
      >
      >O código a seguir supõe que o aplicativo tenha uma implementação do método `isCueInOpportunity`.
      >
      >
      ```
      >- (PTPlacementOpportunity *)preparePlacementOpportunity:(PTTimedMetadata *)timedMetadata 
      >{ 
      >       if ([self isCueInOpportunity:timedMetadata]) 
      >       { 
      >               return [PTPlacementOpportunity advertisementSpliceInOpportunityWithTimedMetadata:timedMetadata]; 
      >       } 
      >       else 
      >       { 
      >               return [super preparePlacementOpportunity:timedMetadata]; 
      >       } 
      >}
      >```

   1. Registre o resolvedor de oportunidade estendida na instância `PTDefaultMediaPlayerClientFactory`.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Clear existing resolver and register the new opportunity resolver 
      [clientFactory clearOpportunityResolvers]; 
      [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
      ```

