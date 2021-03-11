---
description: Em algumas implementações de análise, o aplicativo cliente pode desejar fornecer uma posição de indicador de reprodução diferente da posição relatada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, o indicador de reprodução de cada programa pode ser fornecido de acordo com a hora de início.
title: Implementar atualizações de hora personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Implementar atualizações de hora personalizadas {#implement-custom-time-updates}

Em algumas implementações de análise, o aplicativo cliente pode desejar fornecer uma posição de indicador de reprodução diferente da posição relatada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, o indicador de reprodução de cada programa pode ser fornecido de acordo com a hora de início.

>[!TIP]
>
>Substitua esse método somente se desejar fornecer uma posição do indicador de reprodução diferente da posição padrão.

Para substituir a posição padrão do indicador de reprodução:

```java
vaMetadata.setCurrentTimeUpdateBlock(new VideoAnalyticsMetadata.CurrentTimeUpdateBlock() { 
    @Override 
    public long call() { 
        long range = 500L; 
        Random r = new Random() 
        return (long)(r.nextDouble()*range); 
    } 
});
```

>[!IMPORTANT]
>
>Os valores neste trecho de código são apenas amostras. Você precisa usar valores diferentes para a posição do indicador de reprodução personalizado.