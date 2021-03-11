---
description: Você pode optar por usar comportamentos de publicidade padrão.
title: Usar o comportamento de reprodução padrão
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---


# Usar o comportamento de reprodução padrão{#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de publicidade padrão.

Para usar comportamentos padrão:

* Se você implementar sua própria classe `ContentFactory`, retorne uma nova instância de `DefaultAdPolicySelector` na implementação de `doRetrieveAdPolicySelector`.

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

* Se você não tiver uma implementação personalizada para a classe `ContentFactory`, o TVSDK usará `DefaultAdPolicySelector`.