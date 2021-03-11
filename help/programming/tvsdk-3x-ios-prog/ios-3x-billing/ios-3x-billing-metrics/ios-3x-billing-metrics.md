---
description: Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.
title: Métricas de uso de faturamento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---


# Métricas de faturamento {#billing-metrics}

Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.

Toda vez que gera um evento de início de fluxo, o TVSDK inicia periodicamente mensagens HTTP para enviar mensagens HTTP ao sistema de faturamento do Adobe. O período, conhecido como duração faturável, pode ser diferente para VOD padrão, VOD pro VOD (anúncios intermediários ativados) e conteúdo ao vivo. A duração padrão para cada tipo de conteúdo é de 30 minutos, mas seu contrato com o Adobe determina os valores reais.

As mensagens contêm as seguintes informações:

* Tipo de conteúdo (ao vivo, linear ou VOD)
* URL do conteúdo
* Se os anúncios estão ativados
* Se os anúncios intermediários estão ativados (somente VOD)
* Se o fluxo está protegido pelo DRM
* A versão e a plataforma do TVSDK

O Adobe pré-configura esse acordo, mas se você quiser alterar o acordo, trabalhe com seu representante de Ativação do Adobe.

Para monitorar as estatísticas que o TVSDK envia para o Adobe, obtenha o URL do representante de Ativação do Adobe e use uma ferramenta de captura de rede, por exemplo, Charles, para ver os dados.

## Configurar métricas de faturamento {#configure-billing-metrics}

Se você usar a configuração padrão, não há mais nada que você precise fazer para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante de Ativação do Adobe, use a classe PTBillingMetricsConfiguration para configurar esses parâmetros antes de inicializar o reprodutor de mídia.

A maioria dos clientes deve usar a configuração padrão.

>[!IMPORTANT]
>
>A configuração definida permanece em vigor durante a vida útil do reprodutor de mídia. Depois de inicializar o reprodutor de mídia, não é possível alterar a configuração.

Para configurar métricas de faturamento:

Insira a seguinte amostra de código.

```
PTBillingMetricsConfiguration *billingConfig = [[[PTBillingMetricsConfiguration alloc] init] autorelease]; 
billingConfig.enabled = YES; 
billingConfig.stdVODBillableDurationMinutes = 60.0; 
billingConfig.proVODBillableDurationMinutes = 30.0; 
billingConfig.liveBillableDurationMinutes = 15.0; 
                
// metadata is the PTMetadata instance set on PTMediaPlayerItem 
[metadata setMetadata:billingConfig forKey:PTBillingMetricsConfigurationMetadataKey];
```

## Transmitir métricas de faturamento {#transmit-billing-metrics}

O TVSDK envia métricas de faturamento para o Adobe em um formato XML.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Se você usar uma ferramenta de captura de rede para monitorar as estatísticas transmitidas pelo TVSDK para o Adobe, você verá unidades como as seguintes:

```
<request> 
     <sc_xml_ver>1.0</sc_xml_ver> 
     <reportSuiteID>ptebilling</reportSuiteID> 
     <visitorID>5536C629-5EF7-4F02-8E5D-9FA136CB3CED</visitorID> 
     <pageName>com.adobe.primetime.psdksample</pageName> 
     <timestamp>2016-11-22T18:06:30+0000</timestamp> 
     <userAgent>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</userAgent> 
     <contextData> 
         <billingMetrics> 
                 <contentDuration>1799111</contentDuration> 
                 <contentURL>https%3A%2F%2Fdevimages.apple.com.edgekey.net%2Fstreaming%2Fexamples%2Fbipbop_16x9%2Fbipbop_16x9_variant.m3u8</contentURL> 
                 <contentType>vod</contentType> 
                 <midrollEnabled>true</midrollEnabled> 
                 <tvsdkVersion>1.0.211</tvsdkVersion> 
                 <platform>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</platform> 
                 <publisherID>com.adobe.primetime.psdksample</publisherID> 
                 <adsEnabled>true</adsEnabled> 
                 <type>start</type> 
         </billingMetrics> 
     </contextData> 
</request>
```

As propriedades booleanas `drmProtected`, `adsEnabled` e `midrollEnabled` aparecem somente se forem verdadeiras.