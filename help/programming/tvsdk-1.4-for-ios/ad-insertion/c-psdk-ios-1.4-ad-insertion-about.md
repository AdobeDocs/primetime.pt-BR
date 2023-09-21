---
description: A inserção de anúncios soluciona anúncios de VOD (Video On Demand, vídeo sob demanda), de transmissão ao vivo e de transmissão linear com rastreamento de anúncios e reprodução de anúncio. O TVSDK faz as solicitações necessárias ao servidor de anúncios, recebe informações sobre os anúncios do conteúdo especificado e coloca os anúncios no conteúdo em fases.
title: Inserir anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# Inserir anúncios{#insert-ads}

A inserção de anúncios soluciona anúncios de VOD (Video On Demand, vídeo sob demanda), de transmissão ao vivo e de transmissão linear com rastreamento de anúncios e reprodução de anúncio. O TVSDK faz as solicitações necessárias ao servidor de anúncios, recebe informações sobre os anúncios do conteúdo especificado e coloca os anúncios no conteúdo em fases.

Um *`ad break`* contém um ou mais anúncios reproduzidos em sequência. O TVSDK insere anúncios no conteúdo principal como membros de um ou mais ad breaks.

>[!TIP]
>
>Se o anúncio contiver erros, o TVSDK ignorará o anúncio.

## Resolver e inserir anúncios de VOD {#section_157344F857C64F36B48AD441F6E7FABA}

O TVSDK oferece suporte a vários casos de uso para resolução e inserção de anúncios de VOD.

* Inserção de anúncios antes da exibição, em que os anúncios são inseridos no início do conteúdo.
* Inserção de anúncio intermediário, em que pelo menos um anúncio é inserido no meio do conteúdo.
* Inserção de anúncio após a exibição, em que pelo menos um anúncio é anexado ao final do conteúdo.

O TVSDK resolve os anúncios, insere os anúncios em locais definidos pelo servidor de anúncios e calcula a linha do tempo virtual antes do início da reprodução. Depois que a reprodução começa, nenhuma alteração, como anúncios sendo inseridos ou anúncios inseridos sendo removidos, pode ocorrer.

## Resolver e inserir anúncio dinâmico e linear {#section_A6A1BB262D084462A1D134083556B7CC}

O TVSDK é compatível com vários casos de uso para resolução e inserção de anúncios dinâmicos e lineares.

* Inserção de anúncio antes da exibição, em que pelo menos um anúncio é inserido no início do conteúdo.
* Inserção de anúncio intermediário, em que pelo menos um anúncio é inserido no meio do conteúdo.

O TVSDK resolve os anúncios e os insere quando um ponto de sinalização é encontrado no fluxo ao vivo ou linear. Por padrão, o TVSDK é compatível com as seguintes dicas como marcadores de anúncios válidos ao resolver e inserir anúncios:

* #EXT-X-CUEPOINT
* #EXT-X-AD
* #EXT-X-CUE
* #EXT-X-CUE-OUT

Esses marcadores exigem a identificação do campo de metadados `DURATION` em segundos e o identificador exclusivo da indicação. Por exemplo:

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

Para obter mais informações sobre dicas adicionais, consulte [Inscrever-se em tags personalizadas](../ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-custom-tags-subscribe.md).

## Rastrear anúncio do cliente {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

O TVSDK rastreia anúncios automaticamente para VOD e transmissão ao vivo/linear.

As notificações são usadas para informar seu aplicativo sobre o progresso de um anúncio, incluindo informações sobre quando um anúncio começa e quando termina.

## Implementar um retorno de ad break antecipado {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

Para inserção de anúncios em streaming ao vivo, talvez seja necessário sair de um ad break antes que todos os anúncios do break sejam reproduzidos até a conclusão.

Estes são alguns exemplos de um retorno de ad break antecipado:

* A duração do ad break em determinados eventos esportivos.

  Embora uma duração padrão seja fornecida, se o jogo for retomado antes da interrupção terminar, o ad break deve ser encerrado.
* Um sinal de emergência durante um ad break em um stream ao vivo.

A capacidade de sair de um ad break antecipadamente é identificada por meio de uma tag personalizada no manifesto conhecido como splice ou cue-in tag. O TVSDK permite que o aplicativo assine essas tags de splice para fornecer uma oportunidade de splice.

* Para usar o `#EXT-X-CUE-IN` marque como uma oportunidade de splice e implemente um retorno de ad break antecipado:

   1. Assine a tag.

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. Adicione o resolvedor de oportunidades cue-in.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* Para compartilhar a mesma tag para divisão e divisão:

   1. Se o aplicativo estiver compartilhando a mesma sinalização para indicar cue-out/splice-out e cue-in/splice-in, estenda `PTDefaultAdOpportunityResolver` e implementar a `preparePlacementOpportunity` método.

      >[!TIP]
      >
      >O código a seguir presume que o aplicativo tenha uma implementação para `isCueInOpportunity` método.
      >
      >```
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
      >

   1. Registrar o resolvedor de oportunidades estendidas no `PTDefaultMediaPlayerClientFactory` instância.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Clear existing resolver and register the new opportunity resolver 
      [clientFactory clearOpportunityResolvers]; 
      [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
      ```
