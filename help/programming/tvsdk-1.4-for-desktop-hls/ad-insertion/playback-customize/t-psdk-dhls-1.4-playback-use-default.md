---
description: Você pode optar por usar comportamentos de publicidade padrão.
seo-description: Você pode optar por usar comportamentos de publicidade padrão.
seo-title: Usar o comportamento de reprodução padrão
title: Usar o comportamento de reprodução padrão
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Usar o comportamento de reprodução padrão{#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de publicidade padrão.

Para usar comportamentos padrão:

* Se você implementar sua própria `ContentFactory` classe, retorne uma nova instância do `DefaultAdPolicySelector` em sua implementação do `doRetrieveAdPolicySelector`.

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

* Se você não tiver uma implementação personalizada para a `ContentFactory` classe, o TVSDK usará `DefaultAdPolicySelector`.