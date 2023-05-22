---
description: Em algumas implementações do Analytics, o aplicativo cliente pode querer fornecer uma posição de indicador de reprodução diferente da posição relatada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, o indicador de reprodução de cada programa pode ser fornecido de acordo com seu tempo de início.
title: Implementar atualizações de tempo personalizadas
exl-id: df35d422-d9dc-496d-8f6f-cf34d82ab046
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Implementar atualizações de tempo personalizadas {#implement-custom-time-updates}

Em algumas implementações do Analytics, o aplicativo cliente pode querer fornecer uma posição de indicador de reprodução diferente da posição relatada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, o indicador de reprodução de cada programa pode ser fornecido de acordo com seu tempo de início.

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
>Neste exemplo de código, 500 é apenas um valor de exemplo. Você precisa usar um valor diferente para a posição do indicador de reprodução personalizado.
