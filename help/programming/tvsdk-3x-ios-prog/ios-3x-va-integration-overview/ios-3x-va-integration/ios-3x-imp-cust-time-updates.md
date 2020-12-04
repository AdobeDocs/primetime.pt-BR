---
description: Em algumas implementações do Analytics, o aplicativo cliente pode desejar fornecer uma posição diferente do indicador de reprodução da posição reportada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, cada indicador de reprodução do programa pode ser fornecido em relação ao tempo do start.
seo-description: Em algumas implementações do Analytics, o aplicativo cliente pode desejar fornecer uma posição diferente do indicador de reprodução da posição reportada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, cada indicador de reprodução do programa pode ser fornecido em relação ao tempo do start.
seo-title: Implementar atualizações de tempo personalizadas
title: Implementar atualizações de tempo personalizadas
uuid: 174937ca-3c26-4385-a298-8a01fc93ea20
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Implementar atualizações de hora personalizadas {#implement-custom-time-updates}

Em algumas implementações do Analytics, o aplicativo cliente pode desejar fornecer uma posição diferente do indicador de reprodução da posição reportada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, cada indicador de reprodução do programa pode ser fornecido em relação ao tempo do start.

>[!TIP]
>
>Substitua esse método somente se desejar fornecer uma posição do indicador de reprodução diferente da posição padrão.

Para substituir a posição padrão do indicador de reprodução:

```
vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
    NSInteger random = arc4random() % 500;  
    return CMTimeMakeWithSeconds(random, 1); 
};
```

>[!IMPORTANT]
>
>Nessa amostra de código, 500 é apenas um valor de amostra. Você precisa usar um valor diferente para a posição personalizada do indicador de reprodução.