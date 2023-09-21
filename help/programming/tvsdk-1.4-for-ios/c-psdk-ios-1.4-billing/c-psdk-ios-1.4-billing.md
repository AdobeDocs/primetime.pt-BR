---
description: Para acomodar os clientes que desejam pagar apenas pelo que utilizam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta as métricas de uso e as utiliza para determinar quanto faturar aos clientes.
title: Métricas de cobrança
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Métricas de cobrança {#billing-metrics}

Para acomodar os clientes que desejam pagar apenas pelo que utilizam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta as métricas de uso e as utiliza para determinar quanto faturar aos clientes.

Toda vez que o reprodutor gera um evento de início de fluxo, o TVSDK começa a enviar mensagens HTTP periodicamente para o sistema de cobrança do Adobe. O período, conhecido como duração faturável, pode ser diferente para VOD padrão, pro VOD (anúncios intermediários ativados) e conteúdo ao vivo. A duração padrão para cada tipo de conteúdo é de 30 minutos, mas seu contrato com a Adobe determina os valores reais.

As mensagens contêm as seguintes informações:

* Tipo de conteúdo (ao vivo, linear ou VOD)
* URL de conteúdo
* Se os anúncios estão habilitados
* Se os anúncios intermediários estão ativados (somente VOD)
* Se o fluxo está protegido por DRM
* A versão e a plataforma do TVSDK

O Adobe pré-configura essa organização, mas se você quiser alterar a organização, entre em contato com o representante de Ativação de Adobe.

Para monitorar as estatísticas que o TVSDK envia para o Adobe, obtenha o URL do seu representante de Ativação de Adobe e use uma ferramenta de captura de rede, por exemplo, Charles, para ver os dados.

## Configurar métricas de cobrança {#configure-billing-metrics}

Se você usar a configuração padrão, nada mais precisará ser feito para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante de Ativação de Adobe, use a classe PTBillingMetricsConfiguration para definir esses parâmetros antes de inicializar o reprodutor de mídia.

A maioria dos clientes deve usar a configuração padrão.

>[!IMPORTANT]
>
>A configuração definida permanece em vigor durante a vida útil do reprodutor de mídia. Após inicializar o reprodutor de mídia, não é possível alterar a configuração.

Para configurar métricas de faturamento:

1. Insira a seguinte amostra de código.

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

O TVSDK envia métricas de cobrança para o Adobe em formato XML.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Se você usar uma ferramenta de captura de rede para monitorar as estatísticas que o TVSDK transmite para o Adobe, deverá ver unidades como as seguintes:

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

As propriedades booleanas `drmProtected`, `adsEnabled`, e `midrollEnabled` só aparecerão se forem verdadeiros.
