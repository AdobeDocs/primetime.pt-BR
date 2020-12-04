---
description: O TVSDK do navegador envia métricas de faturamento para o Adobe em um formato XML.
seo-description: O TVSDK do navegador envia métricas de faturamento para o Adobe em um formato XML.
seo-title: Transmitir métricas de faturamento
title: Transmitir métricas de faturamento
uuid: ed2638d2-7894-4840-b31a-51e48e0a3f49
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Transmitir métricas de faturamento{#transmit-billing-metrics}

O TVSDK do navegador envia métricas de faturamento para o Adobe em um formato XML.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Se você usar uma ferramenta de captura de rede para monitorar as estatísticas Transmissões TVSDK do navegador para o Adobe, você verá unidades como as seguintes:

```
<?xml version="1.0" encoding="UTF-8"?>
<request>
    <sc_xml_ver>1.0</sc_xml_ver>
    <reportSuiteID>primesample2</reportSuiteID>
    <visitorID>947310128cb56f41</visitorID>
    <pageURL>https://. . ..m3u8</pageURL>
    <timestamp>2016-4-7T10:1:4</timestamp>
    <contextData>
        <billingMetrics>
            <publisherID>com.adobe.primetime.reference.PrimetimeReference</publisherID>
            <contentType>vod</contentType>
            <adsEnabled>true</adsEnabled>
            <midrollEnabled>true</midrollEnabled>
            <platform>Mac OSX 10.11.5</platform>
            <tvsdkVersion>2,4,0,1559</tvsdkVersion>
            <contentURL>https://. . ..m3u8</contentURL>
        </billingMetrics>
    </contextData>
</request>
```

As propriedades booleanas `drmProtected`, `adsEnabled` e `midrollEnabled` são exibidas somente se forem verdadeiras.