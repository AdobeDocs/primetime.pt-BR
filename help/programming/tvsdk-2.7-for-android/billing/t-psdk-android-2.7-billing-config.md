---
description: Se você usar a configuração padrão, nada mais precisará ser feito para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante de Ativação de Adobe, use a classe BillingMetricsConfiguration para definir esses parâmetros antes de inicializar o reprodutor de mídia.
title: Configurar métricas de cobrança
exl-id: b49b64eb-682b-420f-9681-6e77cdb02c23
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Configurar métricas de cobrança {#configure-billing-metrics}

Se você usar a configuração padrão, nada mais precisará ser feito para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante de Ativação de Adobe, use a classe BillingMetricsConfiguration para definir esses parâmetros antes de inicializar o reprodutor de mídia.

>[!TIP]
>
>A maioria dos clientes deve usar a configuração padrão.

>[!IMPORTANT]
>
>A configuração definida permanece em vigor durante a vida útil do reprodutor de mídia. Após inicializar o reprodutor de mídia, não é possível alterar a configuração.

Para configurar métricas de faturamento:

1. Insira a seguinte amostra de código.

   ```java
   MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
   BillingMetricsConfiguration billingConfig = new BillingMetricsConfiguration(); 
   billingConfig.setEnabled(true); 
   billingConfig.setProVODBillableDurationMinutes(60); 
   billingConfig.setStdVODBillableDurationMinutes(30); 
   billingConfig.setLiveBillableDurationMinutes(15); 
   config.setBillingMetricsConfiguration(billingConfig); 
   mediaPlayer.replaceCurrentResource(mediaResource, config);
   ```
