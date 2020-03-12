---
description: Em algumas implementações do Analytics, o aplicativo cliente pode desejar fornecer uma posição diferente do indicador de reprodução da posição reportada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, o indicador de reprodução de cada programa pode ser fornecido em relação à hora de início.
seo-description: Em algumas implementações do Analytics, o aplicativo cliente pode desejar fornecer uma posição diferente do indicador de reprodução da posição reportada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, o indicador de reprodução de cada programa pode ser fornecido em relação à hora de início.
seo-title: Implementar atualizações de tempo personalizadas
title: Implementar atualizações de tempo personalizadas
uuid: 7f5d46e5-eab6-4bdc-b015-ae27ddb609ce
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Implementar atualizações de tempo personalizadas {#implement-custom-time-updates}

Em algumas implementações do Analytics, o aplicativo cliente pode desejar fornecer uma posição diferente do indicador de reprodução da posição reportada pelo valor localTime do TVSDK. Por exemplo, durante uma reprodução de fluxo linear, o indicador de reprodução de cada programa pode ser fornecido em relação à hora de início.

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
>Os valores neste trecho de código são apenas amostras. Você precisa usar valores diferentes para a posição personalizada do indicador de reprodução.