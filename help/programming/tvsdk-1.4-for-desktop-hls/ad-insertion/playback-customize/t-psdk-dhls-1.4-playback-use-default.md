---
description: Você pode optar por usar comportamentos de anúncio padrão.
title: Usar o comportamento de reprodução padrão
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# Usar o comportamento de reprodução padrão{#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de anúncio padrão.

Para usar comportamentos padrão:

* Se você implementar o seu próprio `ContentFactory` classe, retorne uma nova ocorrência de `DefaultAdPolicySelector` na implementação do `doRetrieveAdPolicySelector`.

  ```
  public class CustomContentFactory extends ContentFactory { 
  
      //... 
      // your custom code for advertising classes 
      //... 
  
      /** 
       * @inheritDoc 
       */ 
      override protected function  
        doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
          return new DefaultAdPolicySelector(item); 
      } 
  }
  ```

* Se você não tiver uma implementação personalizada para o `ContentFactory` classe, usa TVSDK `DefaultAdPolicySelector`.
