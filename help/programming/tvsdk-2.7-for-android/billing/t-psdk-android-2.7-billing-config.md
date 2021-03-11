---
description: Se você usar a configuração padrão, não há mais nada que você precise fazer para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante de Ativação do Adobe, use a classe BillingMetricsConfiguration para definir esses parâmetros antes de inicializar o reprodutor de mídia.
title: Configurar métricas de faturamento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Configurar métricas de faturamento {#configure-billing-metrics}

Se você usar a configuração padrão, não há mais nada que você precise fazer para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante de Ativação do Adobe, use a classe BillingMetricsConfiguration para definir esses parâmetros antes de inicializar o reprodutor de mídia.

>[!TIP]
>
>A maioria dos clientes deve usar a configuração padrão.

>[!IMPORTANT]
>
>A configuração definida permanece em vigor durante a vida útil do reprodutor de mídia. Depois de inicializar o reprodutor de mídia, não é possível alterar a configuração.

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

