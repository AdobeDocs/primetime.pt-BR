---
description: Você pode implementar seus próprios resolvedores de conteúdo com base nos resolvedores padrão.
seo-description: Você pode implementar seus próprios resolvedores de conteúdo com base nos resolvedores padrão.
seo-title: Implementar um resolvedor de conteúdo personalizado
title: Implementar um resolvedor de conteúdo personalizado
uuid: 5f63cc1e-3f4b-460c-9151-2b9d364800e2
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 2%

---


# Implementar um resolvedor de conteúdo personalizado {#implement-a-custom-content-resolver}

Você pode implementar seus próprios resolvedores de conteúdo com base nos resolvedores padrão.

Quando o TVSDK gera uma nova oportunidade, ele repete por meio dos resolvedores de conteúdo registrados procurando por um que seja capaz de resolver essa oportunidade. A primeira que retorna `true` é selecionada para resolver a oportunidade. Se nenhum resolvedor de conteúdo for capaz, essa oportunidade será ignorada. Como o processo de resolução de conteúdo geralmente é assíncrono, o resolvedor de conteúdo é responsável por notificar o TVSDK quando o processo é concluído.

1. Implemente seu próprio `ContentFactory` personalizado, estendendo a interface `ContentFactory` e substituindo `retrieveResolvers`.

   Por exemplo:

   ```java
   class MyContentFactory extends ContentFactory { 
       @Override 
       public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { 
           List<ContentResolver> resolvers = new ArrayList<ContentResolver>(); 
           MediaPlayerItemConfig itemConfig = item.getConfig(); 
           if(itemConfig) { 
               CustomRangeMetadata customRanges = itemConfig.getCustomRangeMetadata(); 
               if (customRanges) { 
                   List<ReplaceTimeRange> timeRanges = customRanges.getTimeRangeList(); 
   
                   if (timeRanges && timeRanges.size() > 0) 
                   { 
                   // CustomRangeResolver is only activated by the presence of CustomRanges in configuration 
                   resolvers.add(new CustomRangeResolver()); 
                   } 
               } 
               AdvertisingMetadata metadata = itemConfig.getAdvertisingMetadata(); 
               if (metadata) { 
                   if (metadata instanceOf AuditudeSettings)  
                       resolvers.add(new AuditudeResolver(getContext());    
                   } 
               } 
           // add your custom resolver if any 
           resolvers.add(MyOpportunityGenerator(item)); 
           return resolvers; 
       } 
       ... 
   } 
   ```

1. Registre `ContentFactory` em `MediaPlayer`.

   Por exemplo:

   ```java
   //Register the custom content factory with the media player 
   MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new MyContentFactory()); 
   
   //Pass this config while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config); 
   
   // OR use MediaPlayerItemLoader to pre-load a resource 
   id = 23; 
   itemLoader.load(resource, id, config);
   ```

1. Passe um objeto `AdvertisingMetadata` para TVSDK da seguinte maneira:
   1. Crie um objeto `AdvertisingMetadata`.
   1. Salve o objeto `AdvertisingMetadata` em `MediaPlayerItemConfig`.

      ```java
      AdvertisingMetadata advertisingMetadata = new AdvertisingMetadata(); 
      
      advertisingMetadata.setDelayAdLoading(true); 
      ... 
      
      mediaPlayerItemConfig.setAdvertisingMetadata(advertisingMetadata); 
      ```

1. Crie uma classe personalizada de resolvedor de anúncios que estende a classe `ContentResolver`.
   1. No resolvedor de publicidade personalizado, substitua `doConfigure`, `doCanResolve`, `doResolve`, `doCleanup`:

      ```java
      void doConfigure(MediaPlayerItem item); 
      boolean doCanResolve(Opportunity opportunity); 
      void doResolve(Opportunity opportunity); 
      void doCleanup();
      ```

      Você obtém seu `advertisingMetadata` do item passado em `doConfigure`:

      ```java
      MediaPlayerItemConfig itemConfig = item.getConfig(); 
      
      AdvertisingMetadata advertisingMetadata =  
        mediaPlayerItemConfig.getAdvertisingMetadata(); 
      ```

   1. Para cada oportunidade de posicionamento, crie um `List<TimelineOperation>`.

      Esta amostra `TimelineOperation` fornece uma estrutura para `AdBreakPlacement`:

      ```java
      AdBreakPlacement( 
          new AdBreak( ads,    // Vector<Ad> 
                       tracker // Content Tracker 
          ), 
          placementInformation // Retrieved from Opportunity 
      ); 
      ```

   1. Depois que os anúncios forem resolvidos, chame uma das seguintes funções:

      * Se a resolução do anúncio for bem-sucedida, chame `process(List<TimelineOperation> proposals)` e `notifyCompleted(Opportunity opportunity)` no `ContentResolverClient`

         ```java
         _client.process(timelineOperations); 
         _client.notifyCompleted(opportunity); 
         ```

      * Se a resolução do anúncio falhar, chame `notifyResolveError` no `ContentResolverClient`

         ```java
         _client.notifyFailed(Opportunity opportunity, PSDKErrorCode error);
         ```

         Por exemplo:

         ```java
         _client.notifyFailed(opportunity, UNSUPPORTED_OPERATION);
         ```

<!--<a id="example_463B718749504A978F0B887786844C39"></a>-->

Este exemplo de resolvedor de anúncios personalizado resolve uma oportunidade e fornece um anúncio simples:

```java
public class CustomContentResolver extends ContentResolver { 
    protected void doConfigure(MediaPlayerItem item){} 
 
    protected boolean doCanResolve(Opportunity opportunity) {  
        return true;  
    } 
 
    protected void doResolve(Opportunity opportunity) { 
        _client.process(createAdBreakPlacementsFor(opportunity.getPlacement())); 
        _client.notifyCompleted(opportunity); 
    } 
 
    private List<TimelineOperation> createAdBreakPlacementsFor(Placement placementInformation) { 
        List<Ad> ads = new ArrayList<Ad>(); 
        AdAsset adAsset = new AdAsset("101", 15000, new MediaResource( 
          "https: . . ..m3u8", MediaResource.Type.HLS, null), null, null); 
 
        Ad ad = Ad.linearFromAsset("101", adAsset, null, null, false); 
        ads.add(ad); 
        AdBreak adBreak = new AdBreak(ads, null, AdInsertionType.CLIENT_INSERTED); 
 
        List<TimelineOperation> result = new ArrayList<TimelineOperation>(); 
 
        result.add(new AdBreakPlacement(placementInformation, adBreak)); 
        return result; 
    } 
 
    protected void doCleanup() {} 
} 
```

