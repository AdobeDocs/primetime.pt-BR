---
description: Você pode implementar seus resolvedores com base nos resolvedores padrão.
title: Implementar uma oportunidade/resolvedor de conteúdo personalizado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# Implemente um resolvedor personalizado de oportunidade/conteúdo {#implement-a-custom-opportunity-content-resolver}

Você pode implementar seus resolvedores com base nos resolvedores padrão.

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. Desenvolva um resolvedor de anúncios personalizado estendendo a classe abstrata `PTContentResolver`.

   `PTContentResolver` é uma interface que deve ser implementada por uma classe de resolvedor de conteúdo. Uma classe abstrata com o mesmo nome também está disponível e lida com a configuração automaticamente (obtendo o delegado).

   >[!TIP]
   >
   >`PTContentResolver` é exposto por meio da  `PTDefaultMediaPlayerClientFactory` classe . Os clientes podem registrar um novo resolvedor de conteúdo estendendo a classe abstrata `PTContentResolver`. Por padrão, e a menos que especificamente removido, um `PTDefaultAdContentResolver` é registrado no `PTDefaultMediaPlayerClientFactory`.

   ```
   @protocol PTContentResolver <NSObject> 
   @required 
   + (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity;  
   //Detector returns YES/NO if it should handle the following placement opportunity 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                 delegate:(id<PTContentResolverDelegate> delegate); 
   - (void)process:(PTPlacementOpportunity *)opportunity; 
   - (void)timeout:(PTPlacementOpportunity *)opportunity;  
   //The timeout method gets invoked if the TVSDK decides that the  
   //PTContentResolver is taking too much time to respond. 
   @end 
   
   @interface PTContentResolver : NSObject <PTContentResolver> 
   
   @property (readonly) id<PTContentResolverDelegate> delegate; 
   @property (readonly) PTMediaPlayerItem *playerItem; 
   
   - (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity; 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                  delegate:(id<PTContentResolverDelegate>) delegate; 
   - (void)process:(NSArray *)opportunities; 
   - (void)cancel:(NSArray *)opportunities; 
   @end
   ```

1. Implemente `shouldResolveOpportunity` e retorne `YES` se ele precisar lidar com o `PTPlacementOpportunity` recebido.
1. Implemente `resolvePlacementOpportunity`, que inicia o carregamento do conteúdo ou anúncios alternativos.
1. Após o carregamento dos anúncios, prepare um `PTTimeline` com as informações sobre o conteúdo a ser inserido.

       Estas são algumas informações úteis sobre linhas do tempo:
   
   * Pode haver vários `PTAdBreak`s de tipos precedentes, intermediário e posterior.

      * Um `PTAdBreak` tem o seguinte:

         * Um `CMTimeRange` com a hora de início e a duração da interrupção.

            Isso é definido como a propriedade range de `PTAdBreak`.

         * `NSArray` de  `PTAd`s.

            Isso é definido como a propriedade ads de `PTAdBreak`.
   * Um `PTAd` representa o anúncio e cada `PTAd` tem o seguinte:

      * Um `PTAdHLSAsset` definido como a propriedade principal do ativo do anúncio.
      * Possivelmente várias instâncias `PTAdAsset` como anúncios clicáveis ou anúncios de banner.

   Por exemplo:

   ```
   NSMutableArray *ptBreaks = [[[NSMutableArray alloc] init] autorelease]; 
   
   // Prepare the primary asset of the ad - links to ad m3u8 
   PTAdHLSAsset *ptAdAsset = [[[PTAdHLSAsset alloc] init] autorelease]; 
   ptAdAsset.source = AD_SOURCE_M3U8; 
   ptAdAsset.id = FAKE_NUMBER_ID; 
   ptAdAsset.format = @"video"; 
   
   // Prepare the ad itself. 
   PTAd *ptAd = [[[PTAd alloc] init] autorelease]; 
   ptAd.primaryAsset = ptAdAsset; 
   ptAd.primaryAsset.ad = ptAd; 
   
   // Prepare the break and add the ad created above. 
   PTAdBreak *ptBreak = [[[PTAdBreak alloc] init] autorelease]; 
   ptBreak.relativeRange = CMTimeRangeMake(BREAK_START_TIME, BREAK_DURATION_VALUE); 
   [ptBreak addAd:ptAd]; 
   
   // Add the break to array of breaks. 
   [ptBreaks addObject:adBreak]; 
   
   // Once all breaks have been prepared, they can be set on timeline 
   PTTimeline *_timeline = [[PTTimeline alloc] init]; 
   _timeline.adBreaks = ptBreaks;
   ```

1. Chame `didFinishResolvingPlacementOpportunity`, que fornece o `PTTimeline`.
1. Registre seu resolvedor de conteúdo/anúncio personalizado na fábrica padrão do reprodutor de mídia, chamando `registerContentResolver`.

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. Se você implementou um resolvedor de oportunidade personalizado, registre-o na fábrica padrão do reprodutor de mídia.

   >[!TIP]
   >
   >Não é necessário registrar um resolvedor de oportunidade personalizado para registrar um resolvedor de conteúdo/anúncios personalizado.

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
   
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
   
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

Quando o reprodutor carrega o conteúdo e é determinado como VOD ou LIVE, uma das seguintes situações ocorre:

* Se o conteúdo for VOD, o resolvedor de conteúdo personalizado será usado para obter a linha do tempo do anúncio de todo o vídeo.
* Se o conteúdo for LIVE, o resolvedor de conteúdo personalizado será chamado sempre que uma oportunidade de posicionamento (ponto de sinalização) for detectada no conteúdo.