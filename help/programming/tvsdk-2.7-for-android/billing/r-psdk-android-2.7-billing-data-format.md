---
description: O TVSDK envia métricas de faturamento para a Adobe em um formato XML.
seo-description: O TVSDK envia métricas de faturamento para a Adobe em um formato XML.
seo-title: Transmitir métricas de faturamento
title: Transmitir métricas de faturamento
uuid: f4a7f50e-f457-434e-bf26-1e06cb15a038
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Transmitir métricas de faturamento {#transmit-billing-metrics}

O TVSDK envia métricas de faturamento para a Adobe em um formato XML.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Se você usar uma ferramenta de captura de rede para monitorar as estatísticas que o TVSDK transmite para a Adobe, você verá unidades como as seguintes:

```xml
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

As propriedades booleanas `drmProtected`, `adsEnabled`e `midrollEnabled` aparecem somente se forem verdadeiras.