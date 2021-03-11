---
description: Em algumas implementações de análise, o aplicativo cliente pode desejar fornecer uma posição de indicador de reprodução diferente da posição relatada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, o indicador de reprodução de cada programa pode ser fornecido de acordo com a hora de início.
title: Implementar atualizações de hora personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Implementar atualizações de hora personalizadas{#implement-custom-time-updates}

Em algumas implementações de análise, o aplicativo cliente pode desejar fornecer uma posição de indicador de reprodução diferente da posição relatada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, o indicador de reprodução de cada programa pode ser fornecido de acordo com a hora de início.

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
   >Neste exemplo de código, 500 é apenas um valor de amostra. Você precisa usar um valor diferente para a posição do indicador de reprodução personalizado.

