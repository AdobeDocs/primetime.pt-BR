---
description: Por padrão, o TVSDK força a reprodução de um ad break quando o usuário busca um ad break. Você pode personalizar o comportamento para ignorar um ad break se o tempo decorrido desde o término de um ad break anterior estiver em um determinado número de minutos.
title: Ignorar ad breaks por um período de tempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Ignorar ad breaks por um período de tempo{#skip-ad-breaks-for-a-period-of-time}

Por padrão, o TVSDK força a reprodução de um ad break quando o usuário busca um ad break. Você pode personalizar o comportamento para ignorar um ad break se o tempo decorrido desde o término de um ad break anterior estiver em um determinado número de minutos.

>[!IMPORTANT]
>
>Quando há uma busca interna para ignorar um anúncio, pode haver uma pequena pausa na reprodução.

O exemplo a seguir de um seletor de política de anúncio personalizado ignora os anúncios nos próximos cinco minutos (hora do relógio da parede) depois que o usuário assiste a um ad break.

1. Estenda o seletor de política de publicidade padrão para substituir o comportamento padrão.

   ```
   /** 
    * Custom ad policy selector. 
    */ 
   public class CustomAdPolicySelector extends DefaultAdPolicySelector { 
   
       /** 
        * Default constructor. 
        * 
        * @param item Associated media player item. 
        */ 
       public function CustomAdPolicySelector(item:MediaPlayerItem) { 
           super(item); 
   
           item.player.addEventListener(AdBreakPlaybackEvent.AD_BREAK_COMPLETED,  
                                        onAdBreakCompleted); 
       } 
   
       override public function selectPolicyForAdBreak(adPolicyInfo:AdPolicyInfo):String { 
           if (shouldPlayAds()) { 
               return super.selectPolicyForAdBreak(adPolicyInfo); 
           } 
   
           return AdBreakPolicy.SKIP; 
       } 
   
       override public function selectAdBreaksToPlay(adPolicyInfo:AdPolicyInfo):Vector.<AdBreakTimelineItem> { 
           if (shouldPlayAds()) { 
               return super.selectAdBreaksToPlay(adPolicyInfo); 
           } 
   
           return new Vector.<AdBreakTimelineItem>(); 
       } 
   
       override public function selectPolicyForSeekIntoAd(adPolicyInfo:AdPolicyInfo):String { 
           if (shouldPlayAds()) { 
               return super.selectPolicyForSeekIntoAd(adPolicyInfo); 
           } 
   
           return AdPolicy.SKIP_TO_NEXT_AD_IN_AD_BREAK; 
       } 
   
       private function onAdBreakCompleted(event:AdBreakPlaybackEvent):void { 
           _lastAdBreakPlayedTime = new Date().valueOf(); 
       } 
   
       private function shouldPlayAds():Boolean { 
           var currentTime:Number = new Date().valueOf(); 
           return isNaN(_lastAdBreakPlayedTime) 
                   ||  (currentTime - _lastAdBreakPlayedTime > _minimumInterval); 
       } 
   
       private var _lastAdBreakPlayedTime:Number = NaN; 
       private var _minimumInterval:Number = 300000; // 5 minutes in milliseconds 
   }
   ```

1. Crie um novo fatory de publicidade que use seu seletor personalizado.

   ```
   public class CustomAdPolicyContentFactory extends DefaultContentFactory { 
   
       private var _adPolicySelector:CustomAdPolicySelector; 
   
       /** 
        * Default constructor. 
        */ 
       public function CustomAdPolicyContentFactory() { 
   
       } 
   
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
       if (!_adPolicySelector) { 
           _adPolicySelector = new CustomAdPolicySelector(item); 
       } 
   
       return _adPolicySelector; 
       } 
   }
   ```

1. Registre a nova classe de fábrica de publicidade a ser usada com o MediaPlayer.

   ```
   var mediaResource:MediaResource =  
     MediaResource.createFromUrl("https://example.org/stream.m3u8", null); 
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     PSDKConfig.retrieveMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomAdPolicyContentFactory(); 
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

