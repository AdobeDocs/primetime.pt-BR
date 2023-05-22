---
description: Você pode implementar seus resolvedores com base nos resolvedores padrão.
title: Implementar um resolvedor de oportunidades/conteúdo personalizado
exl-id: a73f62e1-7e6e-4b16-9bf8-118ec0381c41
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# Implementar um resolvedor de oportunidades/conteúdo personalizado {#implement-a-custom-opportunity-content-resolver}

Você pode implementar seus resolvedores com base nos resolvedores padrão.

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. Desenvolva um resolvedor de anúncios personalizado estendendo o `PTContentResolver` classe abstrata.

   `PTContentResolver` é uma interface que deve ser implementada por uma classe de resolvedor de conteúdo. Uma classe abstrata com o mesmo nome também está disponível e lida com a configuração automaticamente (obtendo o delegado).

   >[!TIP]
   >
   >`PTContentResolver` é exposta através do `PTDefaultMediaPlayerClientFactory` classe. Os clientes podem registrar um novo resolvedor de conteúdo estendendo o `PTContentResolver` classe abstrata. Por padrão, e a menos que especificamente removido, um `PTDefaultAdContentResolver` está registrado na `PTDefaultMediaPlayerClientFactory`.

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

1. Implementar `shouldResolveOpportunity` e retorno `YES` se ele deve lidar com o `PTPlacementOpportunity`.
1. Implementar `resolvePlacementOpportunity`, que inicia o carregamento do conteúdo ou dos anúncios alternativos.
1. Depois que os anúncios forem carregados, prepare um `PTTimeline` com as informações sobre o conteúdo a ser inserido.

       Estas são algumas informações úteis sobre linhas do tempo:
   
   * Pode haver vários `PTAdBreak`s de tipos antes da exibição, durante a exibição e após a exibição.

      * A `PTAdBreak` tem o seguinte:

         * A `CMTimeRange` com a hora de início e a duração da interrupção.

            É definida como a propriedade de intervalo de `PTAdBreak`.

         * `NSArray` de `PTAd`s

            É definida como a propriedade de anúncios de `PTAdBreak`.
   * A `PTAd` representa o anúncio e cada `PTAd` tem o seguinte:

      * A `PTAdHLSAsset` defina como a propriedade principal do ativo do anúncio.
      * Possivelmente múltiplos `PTAdAsset` instâncias como anúncios clicáveis ou anúncios de banner.

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

1. Chame `didFinishResolvingPlacementOpportunity`, que fornece a `PTTimeline`.
1. Registre seu resolvedor de conteúdo/anúncios personalizado na fábrica padrão do reprodutor de mídia, chamando `registerContentResolver`.

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. Se você implementou um resolvedor de oportunidades personalizado, registre-o na fábrica padrão do reprodutor de mídia.

   >[!TIP]
   >
   >Não é necessário registrar um resolvedor de oportunidades personalizado para registrar um resolvedor de conteúdo/anúncios personalizado.

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
   
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
   
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

Quando o reprodutor carrega o conteúdo e determina-se que seja do tipo VOD ou LIVE, uma das situações a seguir ocorre:

* Se o conteúdo for VOD, o resolvedor de conteúdo personalizado será usado para obter a linha do tempo do anúncio do vídeo inteiro.
* Se o conteúdo for EM TEMPO REAL, o resolvedor de conteúdo personalizado será chamado sempre que uma oportunidade de posicionamento (ponto de sinalização) for detectada no conteúdo.
