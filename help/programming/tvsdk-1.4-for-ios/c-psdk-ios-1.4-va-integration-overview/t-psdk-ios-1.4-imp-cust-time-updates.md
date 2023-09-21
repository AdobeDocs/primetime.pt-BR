---
description: Em algumas implementações do Analytics, o aplicativo cliente pode querer fornecer uma posição de indicador de reprodução diferente da posição relatada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, o indicador de reprodução de cada programa pode ser fornecido de acordo com seu tempo de início.
title: Implementar atualizações de tempo personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Implementar atualizações de tempo personalizadas{#implement-custom-time-updates}

Em algumas implementações do Analytics, o aplicativo cliente pode querer fornecer uma posição de indicador de reprodução diferente da posição relatada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, o indicador de reprodução de cada programa pode ser fornecido de acordo com seu tempo de início.

>[!TIP]
>
>Substitua esse método somente se desejar fornecer uma posição do indicador de reprodução diferente da posição padrão.

1. Para substituir a posição padrão do indicador de reprodução:

   ```
   vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
       NSInteger random = arc4random() % 500;  
       return CMTimeMakeWithSeconds(random, 1); 
   };
   ```

   >[!IMPORTANT]
   >
   >Neste exemplo de código, 500 é apenas um valor de exemplo. Você precisa usar um valor diferente para a posição do indicador de reprodução personalizado.
