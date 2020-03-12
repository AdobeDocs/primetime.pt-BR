---
description: Em determinadas implementações do Analytics, o aplicativo cliente pode desejar fornecer uma posição diferente do indicador de reprodução reportado pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo LINEAR, o indicador de reprodução de cada programa pode ser fornecido em relação à hora de início.
seo-description: Em determinadas implementações do Analytics, o aplicativo cliente pode desejar fornecer uma posição diferente do indicador de reprodução reportado pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo LINEAR, o indicador de reprodução de cada programa pode ser fornecido em relação à hora de início.
seo-title: Implementar atualizações de tempo personalizadas
title: Implementar atualizações de tempo personalizadas
uuid: 2b46eca9-3815-4c44-ab5e-21678c35f410
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Implementar atualizações de tempo personalizadas{#implement-custom-time-updates}

Em determinadas implementações do Analytics, o aplicativo cliente pode desejar fornecer uma posição diferente do indicador de reprodução reportado pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo LINEAR, o indicador de reprodução de cada programa pode ser fornecido em relação à hora de início.

>[!TIP]
>
>Substitua este método somente se desejar fornecer uma posição diferente do indicador de reprodução da posição padrão.

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
   >Os valores neste trecho de código são apenas amostras. Você precisa usar valores diferentes para a posição personalizada do indicador de reprodução.

