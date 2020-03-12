---
description: Se você usar a configuração padrão, não há mais nada que você precise fazer para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante do Adobe Enablement, use a classe BillingMetricsConfiguration para configurar esses parâmetros antes de inicializar o player de mídia.
seo-description: Se você usar a configuração padrão, não há mais nada que você precise fazer para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante do Adobe Enablement, use a classe BillingMetricsConfiguration para configurar esses parâmetros antes de inicializar o player de mídia.
seo-title: Configurar métricas de faturamento
title: Configurar métricas de faturamento
uuid: 04d3b53e-f08c-49d0-ba42-5375f1307d2e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Configurar métricas de faturamento{#configure-billing-metrics}

Se você usar a configuração padrão, não há mais nada que você precise fazer para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante do Adobe Enablement, use a classe BillingMetricsConfiguration para configurar esses parâmetros antes de inicializar o player de mídia.

A maioria dos clientes deve usar a configuração padrão.

>[!IMPORTANT]
>
>A configuração definida permanece em vigor durante a vida útil do player de mídia. Depois de inicializar o media player, não é possível alterar a configuração.

Para configurar métricas de faturamento:

* Insira a seguinte amostra de código.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   em que `_player` é uma instância de `AdobePSDK.MediaPlayer` e `_resource` é uma instância de `AdobePSDK.MediaResource`.

