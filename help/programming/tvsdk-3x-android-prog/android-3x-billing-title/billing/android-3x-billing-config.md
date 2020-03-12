---
description: Se você usar a configuração padrão, não há mais nada que você precise fazer para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante do Adobe Enablement, use a classe BillingMetricsConfiguration para configurar esses parâmetros antes de inicializar o player de mídia.
seo-description: Se você usar a configuração padrão, não há mais nada que você precise fazer para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante do Adobe Enablement, use a classe BillingMetricsConfiguration para configurar esses parâmetros antes de inicializar o player de mídia.
seo-title: Configurar métricas de faturamento
title: Configurar métricas de faturamento
uuid: 340439bf-185b-4761-a481-010908842811
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Configurar métricas de faturamento {#configure-billing-metrics}

Se você usar a configuração padrão, não há mais nada que você precise fazer para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante do Adobe Enablement, use a classe BillingMetricsConfiguration para configurar esses parâmetros antes de inicializar o player de mídia.

>[!TIP]
>
>A maioria dos clientes deve usar a configuração padrão.

>[!IMPORTANT]
>
>A configuração definida permanece em vigor durante a vida útil do player de mídia. Depois de inicializar o media player, não é possível alterar a configuração.

Para configurar métricas de faturamento:

Insira a seguinte amostra de código.

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
