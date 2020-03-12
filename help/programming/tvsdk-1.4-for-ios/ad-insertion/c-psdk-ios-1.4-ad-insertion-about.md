---
description: A inserção de anúncios resolve os anúncios para vídeo sob demanda (VOD), para transmissão ao vivo e para transmissão linear com rastreamento de anúncios e reprodução de anúncios. O TVSDK faz as solicitações necessárias para o servidor de anúncios, recebe informações sobre anúncios para o conteúdo especificado e coloca os anúncios no conteúdo em fases.
seo-description: A inserção de anúncios resolve os anúncios para vídeo sob demanda (VOD), para transmissão ao vivo e para transmissão linear com rastreamento de anúncios e reprodução de anúncios. O TVSDK faz as solicitações necessárias para o servidor de anúncios, recebe informações sobre anúncios para o conteúdo especificado e coloca os anúncios no conteúdo em fases.
seo-title: Inserir anúncios
title: Inserir anúncios
uuid: 6fffb340-65ea-4c47-a55b-c0ec4917d37c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Inserir anúncios{#insert-ads}

A inserção de anúncios resolve os anúncios para vídeo sob demanda (VOD), para transmissão ao vivo e para transmissão linear com rastreamento de anúncios e reprodução de anúncios. O TVSDK faz as solicitações necessárias para o servidor de anúncios, recebe informações sobre anúncios para o conteúdo especificado e coloca os anúncios no conteúdo em fases.

Um *`ad break`* contém uma ou mais publicidades que são reproduzidas em sequência. O TVSDK insere publicidades no conteúdo principal como membros de uma ou mais pausas de publicidade.

>[!TIP]
>
>Se o anúncio tiver erros, o TVSDK ignorará o anúncio.

## Resolva e insira anúncios VOD {#section_157344F857C64F36B48AD441F6E7FABA}

O TVSDK suporta vários casos de uso para VOD e solução e inserção de anúncios.

* Inserção de anúncio precedente, onde os anúncios são inseridos no início do conteúdo.
* Inserção de anúncio intermediário, na qual pelo menos um anúncio é inserido no meio do conteúdo.
* Inserção de anúncio posterior, na qual pelo menos um anúncio é anexado ao final do conteúdo.

O TVSDK resolve os anúncios, insere os anúncios em locais definidos pelo servidor de anúncios e calcula a linha do tempo virtual antes do início da reprodução. Após o início da reprodução, nenhuma alteração, como anúncios sendo inseridos ou anúncios inseridos sendo removidos, pode ocorrer.

## Resolver e inserir anúncio ao vivo e linear {#section_A6A1BB262D084462A1D134083556B7CC}

O TVSDK suporta vários casos de uso para a resolução e inserção de anúncios em tempo real e linear.

* Inserção de anúncio precedente, na qual pelo menos um anúncio é inserido no início do conteúdo.
* Inserção de anúncio intermediário, na qual pelo menos um anúncio é inserido no meio do conteúdo.

O TVSDK resolve os anúncios e os insere quando um ponto de sinalização é encontrado no fluxo ao vivo ou linear. Por padrão, o TVSDK oferece suporte às seguintes dicas como marcadores de anúncio válidos ao resolver e inserir anúncios:

* # EXT-X-CUEPOINT
* # EXT-X-AD
* # EXT-X-CUE
* # EXT-X-CUE-OUT

Esses marcadores exigem o campo de metadados `DURATION` em segundos e a ID exclusiva da dica. Por exemplo:

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

Para obter mais informações sobre dicas adicionais, consulte [Assinar tags](../ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-custom-tags-subscribe.md)personalizadas.

## Rastrear anúncio do cliente {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

O TVSDK rastreia automaticamente anúncios para transmissão VOD e transmissão ao vivo/linear.

As notificações são usadas para informar seu aplicativo sobre o progresso de um anúncio, incluindo informações sobre quando um anúncio começa e quando termina.

## Implementar um retorno antecipado de anúncios {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

Para a inserção de um anúncio ao vivo, talvez seja necessário sair de uma quebra de anúncio antes que todos os anúncios na quebra sejam reproduzidos até a conclusão.

Estes são alguns exemplos de retorno antecipado de anúncios:

* A duração do intervalo do anúncio em determinados eventos esportivos.

   Embora seja fornecida uma duração padrão, se o jogo for retomado antes da interrupção, a pausa do anúncio deverá ser encerrada.
* Um sinal de emergência durante uma pausa de anúncio em um fluxo ao vivo.

A capacidade de sair de uma quebra de anúncio é identificada por meio de uma tag personalizada no manifesto conhecida como splice-in ou uma tag de sugestão. O TVSDK permite que o aplicativo assine essas tags splice-in para fornecer uma oportunidade splice-in.

* Para usar a `#EXT-X-CUE-IN` tag como uma oportunidade exclusiva e implementar um retorno antecipado de quebra de anúncio:

   1. Assine a tag .

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. Adicione o resolvedor de oportunidade de entrada.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* Para compartilhar a mesma tag para separação e separação:

   1. Se o aplicativo estiver compartilhando a mesma dica para indicar a saída/separação e a entrada/saída, estenda `PTDefaultAdOpportunityResolver` e implemente o `preparePlacementOpportunity` método.

      >[!TIP]
      >
      >O código a seguir supõe que o aplicativo tenha uma implementação para o `isCueInOpportunity` método.
      >
      >
      >
      >
      >
      ```>
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
      >```       >
      >



   1. Registre o resolvedor de oportunidades estendidas na `PTDefaultMediaPlayerClientFactory` instância.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Clear existing resolver and register the new opportunity resolver 
      [clientFactory clearOpportunityResolvers]; 
      [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
      ```

