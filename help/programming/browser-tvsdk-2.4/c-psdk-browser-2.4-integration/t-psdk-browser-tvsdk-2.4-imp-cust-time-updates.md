---
description: Em algumas implementações do Analytics, o aplicativo cliente pode desejar fornecer uma posição diferente do indicador de reprodução da posição reportada pelo valor LocalTime do TVSDK do navegador.
seo-description: Em algumas implementações do Analytics, o aplicativo cliente pode desejar fornecer uma posição diferente do indicador de reprodução da posição reportada pelo valor LocalTime do TVSDK do navegador.
seo-title: Implementar atualizações de tempo personalizadas
title: Implementar atualizações de tempo personalizadas
uuid: 26a0592c-a47b-4d65-b984-5e51533dcddc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# Implementar atualizações de hora personalizadas{#implement-custom-time-updates}

Em algumas implementações do Analytics, o aplicativo cliente pode desejar fornecer uma posição diferente do indicador de reprodução da posição reportada pelo valor LocalTime do TVSDK do navegador.

Por exemplo, durante uma reprodução de fluxo linear, cada indicador de reprodução do programa pode ser fornecido em relação ao tempo do start.

>[!TIP]
>
>Substitua esse método somente se desejar fornecer uma posição do indicador de reprodução diferente da posição padrão.

Para substituir a posição padrão do indicador de reprodução:

```js
vaMetadata.currentTimeUpdateBlock = function() { 
       return playerPositionInSeconds; 
}; 
```

>[!IMPORTANT]
>
>Os valores neste trecho de código são apenas amostras. Você precisa usar valores diferentes para a posição personalizada do indicador de reprodução.

