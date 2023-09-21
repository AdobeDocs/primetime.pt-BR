---
description: Em determinadas implementações do Analytics, o aplicativo cliente pode querer fornecer uma posição de indicador de reprodução diferente da relatada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo LINEAR, o indicador de reprodução de cada programa pode ser fornecido com relação à hora de início.
title: Implementar atualizações de tempo personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Implementar atualizações de tempo personalizadas{#implement-custom-time-updates}

Em determinadas implementações do Analytics, o aplicativo cliente pode querer fornecer uma posição de indicador de reprodução diferente da relatada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo LINEAR, o indicador de reprodução de cada programa pode ser fornecido com relação à hora de início.

>[!TIP]
>
>Substitua esse método somente se desejar fornecer uma posição do indicador de reprodução diferente da posição padrão.

1. Para substituir a posição padrão do indicador de reprodução:

   ```
   vaMetadata.currentTimeUpdateBlock = function():Number { 
      if (currentTime == 0) { 
          currentTime = getTimer(); 
      } 
      return ((getTimer() - currentTime) / 1000 + 1000); 
   }
   ```

   >[!IMPORTANT]
   >
   >Os valores neste trecho de código são apenas amostras. Você precisa usar valores diferentes para a posição do indicador de reprodução personalizado.
